# EPUB → TXT 转换

## 方法

```bash
python3 -c "
import zipfile, re
from html.parser import HTMLParser

class TextExtractor(HTMLParser):
    def __init__(self):
        super().__init__()
        self.text = []
        self.skip = False
    def handle_starttag(self, tag, attrs):
        if tag in ('script', 'style', 'head'):
            self.skip = True
    def handle_endtag(self, tag):
        if tag in ('script', 'style', 'head'):
            self.skip = False
        if tag in ('p', 'div', 'h1', 'h2', 'h3', 'h4', 'h5', 'h6', 'li', 'br', 'tr'):
            self.text.append('\n')
    def handle_data(self, data):
        if not self.skip:
            self.text.append(data.strip())

epub_path = '<文件路径>'
out_path = '/tmp/book_to_skill.txt'

with zipfile.ZipFile(epub_path) as z:
    container = z.read('META-INF/container.xml').decode('utf-8')
    opf_match = re.search(r'full-path=\"([^\"]+)\"', container)
    opf_path = opf_match.group(1)
    opf = z.read(opf_path).decode('utf-8')
    spine_items = re.findall(r'<itemref idref=\"([^\"]+)\"', opf)
    manifest = {}
    for m in re.finditer(r'<item id=\"([^\"]+)\".*?href=\"([^\"]+)\".*?media-type=\"([^\"]+)\"', opf):
        mid, href, mtype = m.groups()
        manifest[mid] = (href, mtype)
    opf_dir = '/'.join(opf_path.split('/')[:-1])
    if opf_dir: opf_dir += '/'
    all_text = []
    for item_id in spine_items:
        if item_id not in manifest: continue
        href, mtype = manifest[item_id]
        if 'html' not in mtype and 'xhtml' not in mtype and 'xml' not in mtype: continue
        full_path = opf_dir + href
        try:
            content = z.read(full_path).decode('utf-8')
            extractor = TextExtractor()
            extractor.feed(content)
            text = ' '.join(extractor.text)
            text = re.sub(r'\n{3,}', '\n\n', text)
            text = re.sub(r' +', ' ', text)
            all_text.append(text)
        except: pass
    result = re.sub(r'\n{3,}', '\n\n', '\n\n'.join(all_text))
    with open(out_path, 'w', encoding='utf-8') as f:
        f.write(result)
    print(f'Done. {len(result)} chars, {len(result.splitlines())} lines')
"
```

## 验证

```bash
wc -l /tmp/book_to_skill.txt
head -50 /tmp/book_to_skill.txt
```

## 要求

- Python 3 标准库，无需额外安装
- 输出固定路径 `/tmp/book_to_skill.txt`
