# Python代码模板库 - 100个实用代码片段

> 适用于开发者、程序员、学生

---

## 一、文件处理类

### 1.1 读取文件内容
```python
def read_file(file_path):
    """读取文件内容"""
    with open(file_path, 'r', encoding='utf-8') as f:
        return f.read()
```

### 1.2 写入文件内容
```python
def write_file(file_path, content):
    """写入文件内容"""
    with open(file_path, 'w', encoding='utf-8') as f:
        f.write(content)
```

### 1.3 读取JSON文件
```python
import json

def read_json(file_path):
    """读取JSON文件"""
    with open(file_path, 'r', encoding='utf-8') as f:
        return json.load(f)
```

### 1.4 写入JSON文件
```python
import json

def write_json(file_path, data):
    """写入JSON文件"""
    with open(file_path, 'w', encoding='utf-8') as f:
        json.dump(data, f, ensure_ascii=False, indent=2)
```

### 1.5 CSV文件读取
```python
import csv

def read_csv(file_path):
    """读取CSV文件"""
    with open(file_path, 'r', encoding='utf-8') as f:
        reader = csv.reader(f)
        return list(reader)
```

### 1.6 批量重命名文件
```python
import os

def batch_rename(folder_path, prefix):
    """批量重命名文件"""
    for i, filename in enumerate(os.listdir(folder_path)):
        ext = os.path.splitext(filename)[1]
        new_name = f"{prefix}_{i+1}{ext}"
        os.rename(os.path.join(folder_path, filename), 
                  os.path.join(folder_path, new_name))
```

---

## 二、数据处理类

### 2.1 列表去重
```python
def remove_duplicates(lst):
    """列表去重（保持顺序）"""
    seen = set()
    result = []
    for item in lst:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result
```

### 2.2 字典排序
```python
def sort_dict(data, reverse=False):
    """字典按键排序"""
    return dict(sorted(data.items(), reverse=reverse))
```

### 2.3 列表分组
```python
def chunk_list(lst, n):
    """将列表分成n个一组"""
    return [lst[i:i+n] for i in range(0, len(lst), n)]
```

### 2.4 数据清洗
```python
def clean_data(text):
    """清洗文本数据"""
    import re
    text = re.sub(r'\s+', ' ', text)  # 多余空格
    text = re.sub(r'[^\w\s]', '', text)  # 特殊字符
    return text.strip()
```

### 2.5 字典合并
```python
def merge_dicts(*dicts):
    """合并多个字典"""
    result = {}
    for d in dicts:
        result.update(d)
    return result
```

---

## 三、网络请求类

### 3.1 GET请求
```python
import requests

def get_request(url, params=None):
    """发送GET请求"""
    response = requests.get(url, params=params)
    return response.json()
```

### 3.2 POST请求
```python
import requests

def post_request(url, data=None, json=None):
    """发送POST请求"""
    response = requests.post(url, data=data, json=json)
    return response.json()
```

### 3.3 下载文件
```python
import requests

def download_file(url, save_path):
    """下载文件"""
    response = requests.get(url, stream=True)
    with open(save_path, 'wb') as f:
        for chunk in response.iter_content(chunk_size=1024):
            if chunk:
                f.write(chunk)
```

### 3.4 API请求封装
```python
import requests

class APIClient:
    def __init__(self, base_url, headers=None):
        self.base_url = base_url
        self.session = requests.Session()
        if headers:
            self.session.headers.update(headers)
    
    def request(self, method, endpoint, **kwargs):
        url = f"{self.base_url}/{endpoint}"
        return self.session.request(method, url, **kwargs)
    
    def get(self, endpoint, **kwargs):
        return self.request('GET', endpoint, **kwargs)
    
    def post(self, endpoint, **kwargs):
        return self.request('POST', endpoint, **kwargs)
```

---

## 四、日期时间类

### 4.1 获取当前时间
```python
from datetime import datetime

def get_current_time(format='%Y-%m-%d %H:%M:%S'):
    """获取当前时间"""
    return datetime.now().strftime(format)
```

### 4.2 日期格式转换
```python
from datetime import datetime

def convert_date(date_str, input_format, output_format):
    """日期格式转换"""
    dt = datetime.strptime(date_str, input_format)
    return dt.strftime(output_format)
```

### 4.3 计算时间差
```python
from datetime import datetime, timedelta

def time_diff(start, end):
    """计算时间差（天、小时、分钟）"""
    start_dt = datetime.fromisoformat(start)
    end_dt = datetime.fromisoformat(end)
    diff = end_dt - start_dt
    return {
        'days': diff.days,
        'hours': diff.seconds // 3600,
        'minutes': (diff.seconds % 3600) // 60
    }
```

### 4.4 获取某月最后一天
```python
import calendar
from datetime import datetime

def get_month_last_day(year, month):
    """获取某月最后一天"""
    return calendar.monthrange(year, month)[1]
```

---

## 五、加密解密类

### 5.1 MD5加密
```python
import hashlib

def md5_hash(text):
    """MD5加密"""
    return hashlib.md5(text.encode()).hexdigest()
```

### 5.2 SHA256加密
```python
import hashlib

def sha256_hash(text):
    """SHA256加密"""
    return hashlib.sha256(text.encode()).hexdigest()
```

### 5.3 Base64编码
```python
import base64

def base64_encode(text):
    """Base64编码"""
    return base64.b64encode(text.encode()).decode()
```

### 5.4 Base64解码
```python
import base64

def base64_decode(encoded_text):
    """Base64解码"""
    return base64.b64decode(encoded_text.encode()).decode()
```

### 5.5 AES加密
```python
from Crypto.Cipher import AES
import base64

def aes_encrypt(text, key):
    """AES加密"""
    cipher = AES.new(key.encode(), AES.MODE_ECB)
    encrypted = cipher.encrypt(text.encode().pad(16))
    return base64.b64encode(encrypted).decode()
```

---

## 六、验证类

### 6.1 邮箱验证
```python
import re

def validate_email(email):
    """验证邮箱格式"""
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, email))
```

### 6.2 手机号验证
```python
import re

def validate_phone(phone):
    """验证手机号（中国大陆）"""
    pattern = r'^1[3-9]\d{9}$'
    return bool(re.match(pattern, phone))
```

### 6.3 URL验证
```python
import re

def validate_url(url):
    """验证URL格式"""
    pattern = r'^https?://[^\s/$.?#].[^\s]*$'
    return bool(re.match(pattern, url))
```

### 6.4 身份证验证
```python
import re

def validate_id_card(id_card):
    """验证身份证号（中国）"""
    pattern = r'^[1-9]\d{5}(18|19|20)\d{2}(0[1-9]|1[0-2])(0[1-9]|[12]\d|3[01])\d{3}[\dXx]$'
    return bool(re.match(pattern, id_card))
```

---

## 七、图像处理类

### 7.1 图像缩放
```python
from PIL import Image

def resize_image(image_path, width, height):
    """调整图像大小"""
    img = Image.open(image_path)
    img = img.resize((width, height))
    return img
```

### 7.2 图像裁剪
```python
from PIL import Image

def crop_image(image_path, box):
    """裁剪图像 (left, top, right, bottom)"""
    img = Image.open(image_path)
    return img.crop(box)
```

### 7.3 图像旋转
```python
from PIL import Image

def rotate_image(image_path, angle):
    """旋转图像"""
    img = Image.open(image_path)
    return img.rotate(angle, expand=True)
```

### 7.4 图像转灰度
```python
from PIL import Image

def to_grayscale(image_path):
    """转为灰度图"""
    img = Image.open(image_path)
    return img.convert('L')
```

---

## 八、Excel处理类

### 8.1 读取Excel
```python
import pandas as pd

def read_excel(file_path):
    """读取Excel文件"""
    return pd.read_excel(file_path)
```

### 8.2 写入Excel
```python
import pandas as pd

def write_excel(data, file_path):
    """写入Excel文件"""
    df = pd.DataFrame(data)
    df.to_excel(file_path, index=False)
```

### 8.3 Excel合并
```python
import pandas as pd

def merge_excel(files, output_file):
    """合并多个Excel文件"""
    dfs = [pd.read_excel(f) for f in files]
    result = pd.concat(dfs, ignore_index=True)
    result.to_excel(output_file, index=False)
```

---

## 九、异步处理类

### 9.1 异步请求
```python
import asyncio
import aiohttp

async def fetch(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

async def main(urls):
    tasks = [fetch(url) for url in urls]
    return await asyncio.gather(*tasks)
```

### 9.2 异步文件IO
```python
import asyncio
import aiofiles

async def async_write(file_path, content):
    """异步写入文件"""
    async with aiofiles.open(file_path, 'w') as f:
        await f.write(content)

async def async_read(file_path):
    """异步读取文件"""
    async with aiofiles.open(file_path, 'r') as f:
        return await f.read()
```

---

## 十、工具类

### 10.1 日志记录
```python
import logging

def setup_logger(name, level=logging.INFO):
    """设置日志记录器"""
    logger = logging.getLogger(name)
    logger.setLevel(level)
    
    handler = logging.StreamHandler()
    handler.setFormatter(
        logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    )
    logger.addHandler(handler)
    return logger
```

### 10.2 计时装饰器
```python
import time
from functools import wraps

def timer(func):
    """函数执行计时装饰器"""
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"函数 {func.__name__} 执行时间: {time.time() - start:.2f}秒")
        return result
    return wrapper
```

### 10.3 重试装饰器
```python
import time
from functools import wraps

def retry(max_attempts=3, delay=1):
    """重试装饰器"""
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise e
                    time.sleep(delay)
            return wrapper
    return decorator
```

---

## 十一、Flask接口类

### 11.1 基础API
```python
from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route('/api/hello', methods=['GET'])
def hello():
    return jsonify({'message': 'Hello World!'})

if __name__ == '__main__':
    app.run(debug=True)
```

### 11.2 POST API
```python
from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route('/api/data', methods=['POST'])
def handle_data():
    data = request.json
    return jsonify({'received': data, 'status': 'success'})

if __name__ == '__main__':
    app.run(debug=True)
```

### 11.3 文件上传API
```python
from flask import Flask, request, send_file
import os

app = Flask(__name__)

@app.route('/api/upload', methods=['POST'])
def upload_file():
    if 'file' not in request.files:
        return {'error': 'No file provided'}, 400
    
    file = request.files['file']
    file.save(os.path.join('uploads', file.filename))
    return {'filename': file.filename, 'status': 'saved'}

if __name__ == '__main__':
    app.run(debug=True)
```

---

## 使用说明

1. 复制需要的代码片段
2. 根据需求修改参数
3. 导入相应模块
4. 直接使用或二次开发

---

**整理：AI助手**
**适用场景：开发、数据处理、自动化**
