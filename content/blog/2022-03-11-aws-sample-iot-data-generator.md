---
title: AWS Sample IoT Data Generator
date: 2022-03-11T08:09:41.625Z
tags:
  - aws
  - cli
  - python2
  - pip2
  - iot
draft: false
---
<!--StartFragment-->

Có một cái ví dụ về việc giả lập dữ liệu IoT bắn ra từ các thiết bị ở đây: <https://github.com/aws-samples/sbs-iot-data-generator>

Mới đọc qua thì cũng hay, và thấy chỉ có duy nhất 1 file .py nên nghĩ là ale hấp cứ download về rồi chạy python *filename.py* là OK thôi, ai dè cũng lắm truân chuyên. Nên thôi lỡ rồi cũng gui lại đây để sau này tiện copy khi có cần nữa.

Mình triển khai trên Ubuntu 20.04.4 LTS, cần có những thứ này để tiếp tục:

* Amazon Web Services account: để lấy Access keys (access key ID and secret access key)
* AWS Command Line Interface (CLI): chạy lệnh `aws configure` rồi điền các thông tin cần thiết, bao gồm Access key ở trên.
* Python: phiên bản 2.7.18, giờ cài phiên bản 3.x chạy source này báo lỗi `SyntaxError: Missing parentheses in call to 'print'. Did you mean print(data)?`
* Pip2:

`sudo add-apt-repository universe sudo apt update curl <https://bootstrap.pypa.io/pip/2.7/get-pip.py> --output get-pip.py # Fetch get-pip.py for python 2.7 python2 get-pip.py pip2 --version`

* boto3: [](https://aws.amazon.com/sdk-for-python/)<https://aws.amazon.com/sdk-for-python/>, cài xong pip2 thì chạy `pip2 install boto3`

Sau khi setup xong thì chạy `python2 sbs.py` thôi.

**Phong Vân**

<!--EndFragment-->