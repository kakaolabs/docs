Server cung cấp 2 API

# Get list category `/sms/v1/categories/`

## GET parameters
+ `api_key`: api key cuả client
+ `api_sig`: cách tính API signature được ghi trong tài liệu bảo mật API
+ `time`: epoch time cuả hệ thống (bắt buộc phải thêm để signature của API là khác nhau)

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
+ `image_url`: Image URL for category
+ `index`: Int client sử dụng trường index để sắp xếp thứ tự của các category.
   Category có index càng thấp thì càng hiển thị đầu tiên.
   Nếu các category có cùng index, thì sắp xếp theo tên của category
+ `data`: Nếu type là 0, thì data sẽ là list các sub category.
   Nếu không có subcategory hoặc type là 1, data sẽ là []
   Mỗi một subcategory sẽ có 3 trường
      + `name`: tên của subcategory
      + `id`: id của subcategory
      + `image_url`: Image URL của subcategory
      + `index`: index của các subcategory. Thứ tự sắp xếp như sắp xếp category


# Get thông tin của một subcategory `/sms/v1/subcategory/<subcategory_id>/`
VD: `/sms/v1/subcategory/12/`

## GET parameters
+ `api_key`: api key cuả client
+ `api_sig`: cách tính API signature được ghi trong tài liệu bảo mật API
+ `size`: (optional) giá trị mặc định là 50. Đây là số lượng các tin nhắn sẽ trả về. Giá trị lớn nhất của size là 50
+ `offset`: (optional) gía trị mặc định là 0.
   Server sẽ trả về `size` dữ liệu từ `offset` từ vị trí offset
+ `time`: epoch time cuả hệ thống (bắt buộc phải thêm để signature của API là khác nhau)

## Dữ liệu trả về là một mảng các JSON object. Mỗi object sẽ bao gồm các trường
+ `id`: ID của một tin nhắn
+ `content`: tên của category hoặc subcategory
+ `votes`: số lần được vote (mặc định bằng 0)
+ `index`: Client sử dụng index để sắp xếp các sms content.
  Index càng thấp, thì sms content càng hiện thị ở đầu.
  Sắp xếp theo thứ tự: index asc, votes desc, content asc
