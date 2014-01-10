# Vì sao cần bảo mật
Để bảo mật API (tránh việc user bình thường khi biết API endpoint có thể gọi tới
API của hệ thống, và crawl hết dữ liệu), client sẽ được cung cấp 2 tham số:

+ API_KEY
+ API_SECRET

Cả 2 tham số này đều được hardcode trong code của client.
Khi client request lên server, client sẽ truyền lên 2 tham số

+ `api_key`: API_KEY client được assign
+ `api_sig`: Signature của request

# Cách bảo mật API:

Thuật toán tính signature của request:

Mỗi một request gửi lên sẽ bao gồm các GET, POST parameters (các PUT, PATCH
parameters được coi như là POST parameters)
Tất cả các GET và POST param sẽ được đưa vào một dictionary.
Dictionary được sắp xếp theo thứ tự bảng chữ cái của các key.

    # data = dictionary of GET and POST except api_sig parameters
    sorted_key = sorted(data.keys)
    request_string = url_enpoint + ",".join("%s=%s" % (key, data[key]) for key in sorted_key) + API_SECRET

    # need encode UTF8 because sometime we want to
    api_sig = SHA1(request_string.encode('utf-8'))

VD:

    API_KEY = '0b0c06cc-c4e4-443e-b0d1-3c377034ce92'
    API_SECRET = 'f97a86e8-e605-4dac-98dd-909cf6da080b'
    request:

    curl -XPOST  "http://smscute.kakaolabs.com/v1/user/signup/?api_key=0b0c06cc-c4e4-443e-b0d1-3c377034ce92&time=1389343923" -d "username=kiennt&password=k"

    data = {
        "api_key": "0b0c06cc-c4e4-443e-b0d1-3c377034ce92",
        "time": 1389343923,
        "username": "kiennt",
        "password": "k"
    }
    sorted_keys = ["api_key", "password", "time", "username"]
    request_string = "/v1/user/signup/api_key=0b0c06cc-c4e4-443e-b0d1-3c377034ce92time=1389343923username=kienntpassword=kf97a86e8-e605-4dac-98dd-909cf6da080b"
    api_sig = SHA1(request_string) # e3e40dce69ebfec6e1ce70005ceba3e48d0abcc2



