Server cung cấp 2 API

# Get list category `/sms/v1/categories/`

## GET parameters
+ `api_key`: api key cuả client
+ `api_sig`: cách tính API signature được ghi trong tài liệu bảo mật API
+ `time`: epoch time cuả hệ thống

## Dữ liệu trả về là một mảng các JSON object. Mỗi object sẽ bao gồm các trường
+ `type`: kiểu int. Nhận giá trị 0 hoặc 1
   - 0: category
   - 1: subcategory
  Category và subcategory khác nhau ở điểm. Subcategory chỉ chứa các tin nhắn sms cụ thể.
  Còn category thì chứa các category/subcategory khác
  VD:
    Category: tình yêu chứa các subcategory: tán gái, tỏ tình, gửi người yêu
    Subcategory: tán gái sẽ chứa cụ thể các tin nhắn
+ `name`: tên của category hoặc subcategory
+ `id`: ID cụ thể của các category/hoặc subcategory
+ `data`: Nếu type là 0, thì data sẽ là list các sub category.
   Nếu không có subcategory hoặc type là 1, data sẽ là []
   Mỗi một subcategory sẽ có 3 trường
      + `name`: tên của subcategory
      + `id`: id của subcategory


# Get thông tin của một subcategory `/sms/v1/subcategory/<subcategory_id>/`
VD: `/sms/v1/subcategory/12/`

## GET parameters
+ `api_key`: api key cuả client
+ `api_sig`: cách tính API signature được ghi trong tài liệu bảo mật API
+ `time`: epoch time cuả hệ thống
+ `from_id`: (optional) giá trị mặc định bằng 0. Tất cả các tin nhắn trả về sẽ có ID lớn hơn from_id
+ `size`: (optional) giá trị mặc định là 50. Đây là số lượng các tin nhắn sẽ trả về. Giá trị lớn nhất của size là 50

## Dữ liệu trả về là một mảng các JSON object. Mỗi object sẽ bao gồm các trường
+ `id`: ID của một tin nhắn
+ `content`: tên của category hoặc subcategory
+ `votes`: số lần được vote (mặc định bằng 0)
