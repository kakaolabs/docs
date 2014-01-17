# Các client khi make request lên server nên có phần log để log ra dữ liệu đã
request, như thế sẽ giúp server trong quá trình debug


Dữ liệu log nên có dạng CURL. CURL là dạng command line có thể gõ trực tiếp
trong terminal, như thế sẽ giúp cả client và server check được dữ liệu trả về
của server mà không cần sử dụng app

VD:

## GET request

    http://api.kakaolabs.com/v1/user/134/?api_sig=123&api_key=456

    CURL command:
    curl -XGET "http://api.kakaolabs.com/v1/user/134/?api_sig=123&api_key=456"


## POST request
POST request giống như GET request, nhưng cần thêm data.
Data được thêm bằng tham số -d

    http://api.kakaolabs.com/v1/user/login/?api_sig=123&api_key=456
    data: username=kiennt password=k

    CURL command:
    curl -XPOST "http://api.kakaolabs.com/v1/user/134/?api_sig=123&api_key=456" -d "username=kiennt&password=k"

## Header
Đôi khi chúng ta cũng muốn thay đổi cả header của request.
Ví dụ sử dụng header của request để set UserAgent như là version của app.
Header có thể được thêm bằng cách sử dụng tham số -H

    http://api.kakaolabs.com/v1/user/login/?api_sig=123&api_key=456
    data: username=kiennt password=k
    header: UserAgent: smscute-v1.0

    CURL command:
    curl -XPOST "http://api.kakaolabs.com/v1/user/134/?api_sig=123&api_key=456" -d "username=kiennt&password=k" -H "UserAgent: smscute-v1.0"
