# CS331.M22-KHCL  
<h1 align="center">Thị giác máy tính nâng cao</h1>
 
<!-- PROJECT LOGO -->
<div align="center">
  <h3 align="center">COURSE PROJECT</h3>
  <a>
    <img src="https://www.cio.com/wp-content/uploads/2021/12/ai-in-automotive_1280x609-100790232-orig.jpeg?quality=50&strip=all" alt="Logo" width="640" height="304.5">
  </a>

  <h3 align="center">AN IN-CAR CAMERA SYSTEM FOR TRAFFIC SIGN DETECTION AND RECOGNITION</h3>

  <p align="center">
    USING RETINA NET, FASTERCNN, YOLOv5
    </br>
    </br>
    <a href="https://www.miai.vn/2021/04/01/xay-dung-he-thong-nhan-dien-bien-bao-giao-thong-bang-retinanet/">RETINANET</a>
    ·
    <a href="https://viblo.asia/p/deep-learning-thuat-toan-faster-rcnn-voi-bai-toan-phat-hien-duong-luoi-bo-faster-rcnn-object-detection-algorithm-for-nine-dash-line-detection-bJzKmREOZ9N">FASTERRCNN</a>
    ·
    <a href="https://viblo.asia/p/tong-hop-kien-thuc-tu-yolov1-den-yolov5-phan-1-naQZRRj0Zvx">YOLOv5</a></br>
    <a href="https://drive.google.com/drive/folders/1WT62tiCCsOyEOoRtkzo4n9BwpufK0zmb">LINK PROJECT</a>
  </p>
</div>

<table align="center">
 <tr>
  <th>MSSV</th>
  <th>Họ và tên</th>
  <th>Github</th>
  <th>Email</th>
 </tr>
 <tr>
  <td>19521332</td>
  <td>Lê Thành Đạt</td>
  <td><a href="https://github.com/ledat1205">ledat1205<a></td>
  <td><a href="19521332@gmail.uit.edu.vn">19521332@gmail.uit.edu.vn<a></td>
 </tr>
 <tr>
  <td>19521332</td>
  <td>Vũ Tuấn Anh</td>
  <td><a href="https://github.com/TuanAnhlewlew">TuanAnhlewlew<a></td>
  <td><a href="19521228@gmail.uit.edu.vn">19521228@gmail.uit.edu.vn<a></td>
 </tr>
 <tr>
  <td>19520008</td>
  <td>Cao Tuấn Anh</td>
  <td><a href="https://github.com/tuananh2604">tuananh2604<a></td>
  <td><a href="1950008@gmail.uit.edu.vn">1950008@gmail.uit.edu.vn<a></td>
 </tr>
</table>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#Tổng-quan">Tổng quan</a>
    </li>
    <li>
      <a href="#Mô-tả-bài-toán">Mô tả bài toán</a>
      <ul>
        <li><a href="#Input">Input</a></li>
        <li><a href="#Output">Output</a></li>
      </ul>
    </li>
    <li><a href="#Khái-quát-bộ-dữ-liệu">Khái quát bộ dữ liệu</a></li>
    <li><a href="#Xây-dựng-bộ-dữ-liệu">Xây dựng bộ dữ liệu</a>
      <ul>
         <li><a href="#Các-tiêu-chí-đề-ra">Các tiêu chí đề ra</a>
      </ul>
      <ul>
         <li><a href="#Label-dữ-liệu-sử-dụng-LabelImg">Label dữ liệu sử dụng LabelImg</a>
      </ul>
      <ul>
         <li><a href="#Phân-bố-lớp-trong-bộ-dữ-liệu">Phân bố lớp trong bộ dữ liệu</a>
      </ul>
    </li>
    <li><a href="#Hướng-tiếp-cận">Hướng tiếp cận</a></li>
      <ul>
         <li><a href="#Giới-thiệu-về-RetinaNet">Giới thiệu về RetinaNet</a>
      </ul>
      <ul>
         <li><a href="#Giới-thiệu-về-FasterRCNN">Giới thiệu về FasterRCNN</a>
      </ul>
      <ul>
         <li><a href="#Giới-thiệu-về-YOLOv5">Giới thiệu về YOLOv5</a>
      </ul>
    <li><a href="#Training-và-Đánh-giá-model">Training và Đánh giá model</a></li>
    <li><a href="#So-sánh">So sánh</a></li>
  </ol>
</details>

<!-- TỔNG QUAN -->
## Tổng quan

<div align="center">
 <a>
    <img src="https://storage.googleapis.com/enterknow.com/data-contents/2021/09/autonomous-driving.jpg" alt="Logo" width="600" height="375">
 </a>
</div>
 
Trong thời đại ngày càng phát triển, việc giúp cho máy tính có thể nhận diện các đối tượng giống như con người ngày càng trở nên quan trọng. Và nhóm chúng em đã nghiên cứu để giúp máy tính có thể nhận diện được biển báo giao thông ứng dụng trong phát triển xe tự hành. Qua đó có thể giúp xe tự hành có thể tự lưu thông trên đường 1 cách an toàn hơn mà không gây ảnh hưởng đến người lái xe cũng như những người tham gia giao thông trên cùng tuyến đường.

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- MÔ TẢ BÀI TOÁN -->
## Mô tả bài toán
### Input
Một hình ảnh chứa biển báo giao thông dưới góc nhìn của camera hành trình ô tô.

### Output
Hình ảnh chứa bounding box các loại biển báo giao thông và nhãn cho các bounding box đó.

Detect 5 loại biển chính:
* Cấm đi ngược chiều.
* Hướng đi phải vòng sang phải.
* Giao nhau với đường không ưu tiên.
* Cấm đỗ xe.
* Người đi bộ.

<div align="center">
 <a>
    <img src="https://thietbigiaothong247.com/wp-content/uploads/2017/04/bien-cam-di-nguoc-chieu-400x400.jpg" alt="Logo" width="70" height="70">
 </a>
 <a>
    <img src="http://www.baoholaodong247.com/Portals/26918/302a.jpg" alt="Logo" width="70" height="70">
 </a>
 <a>
    <img src="https://alohoc.com/data/upload/2019/0217/207c-giao-nhau-voi-duong-khong-uu-tien-500x500.jpg?ver=1655170526" alt="Logo" width="70" height="70">
 </a>
 <a>
    <img src="https://thuthuat.taimienphi.vn/cf/Images/gl/2019/4/5/bien-bao-cam-do-xe-p-131a-p-131b-p-131c.jpg" alt="Logo" width="70" height="70">
 </a>
 <a>
    <img src="http://baoholaodong247.com/DesktopModules/Store/Thumbnail.aspx?IP=/Portals/26918/423b.jpg&IW=292" alt="Logo" width="70" height="70">
 </a>
</div>

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- KHÁI QUÁT BỘ DỮ LIỆU -->
## Khái quát bộ dữ liệu

Tổng cộng 3465 bức ảnh được trích xuất ra từ các đoạn video ngắn của camera hành trình ô tô. 

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- KHÁI QUÁT BỘ DỮ LIỆU -->
## Xây dựng bộ dữ liệu
### Các tiêu chí đề ra:
* Hình được lấy từ mặt trước biển báo và phải chứa ít nhất 1 biển báo.
* Các biển báo ở tầm trung cần phải rõ ràng, không bị nhòe, không quá mờ, có thể nhận diện được nội dung bên trong biển báo bằng mắt thường.
* Biển báo có thể tối hoặc ngược sáng nhưng vẫn phải nhìn được nội dung biển báo.
* Biển báo từ góc nhìn của camera hành trình của xe ô tô.

### Label dữ liệu sử dụng LabelImg:
* Gán nhãn với định dạng YOLO. Định dạng YOLO là định dạng file text và mỗi bbox được xác định bằng một bộ 5 số lần lượt là tên lớp (class), tọa độ tâm của bbox (x, y), chiều ngang và chiều cao của bbox (w, h).
* Với tổng cộng 6 class: 5 biển chính và 1 biển khác

### Phân bố lớp trong bộ dữ liệu
* Cấm đi ngược chiều: 1716
* Hướng đi phải vòng sang phải: 1069
* Giao nhau với đường không ưu tiên: 362
* Người đi bộ: 593
* Cấm đỗ xe: 678
* Biển khác: 2183

<p align="right">(<a href="#top">back to top</a>)</p>

## Hướng tiếp cận
<div align="center">
    Chúng em sẽ tiếp cận bài toán với 3 mô hình là: </br>
         RetinaNet </br>
         FasterRCNN </br>
         YOLOv5
</div>

### Giới thiệu về RetinaNet
<h3>RetinaNet:</h3>
RetinaNet sử dụng ResNet và FPN như là backbone để trích xuất đặc trưng của ảnh. </br>
Ngoài ra sử dụng hàm focal loss nhằm giảm thiểu mất mát của những trường hợp dễ dự báo do đó tập trung hơn vào những trường hợp khó dự báo. Nhờ đó cải thiện được độ chính xác.
<div align="center">
     <a>
          <img src="https://developers.arcgis.com/python/guide/images/retinanet.png" alt="Logo" width="1069" height="321">
     </a>
</div>

<h3>Feature Pyramid Network:</h3>
Feature extractor kết hợp giữa Resnet + FPN, có tác dụng trích lọc đặc trưng và trả về các feature map. Mạng FPN (Featuer Pyramid Network) sẽ tạo ra một multi-head dạng kim tự tháp.
<div align="center">
     <a>
          <img src="https://miro.medium.com/max/1380/1*D_EAjMnlR9v4LqHhEYZJLg.png" alt="Logo" width="690" height="395">
     </a>
</div>

<h3>Focal Loss: </h3>
<div align="center">
     <a>
          <img src="https://miro.medium.com/max/458/1*VlXKyklT9IR0yjF1olGUig.png" alt="Logo" width="210" height="60"> </br>
     </a>
     <a>
          <img src="https://miro.medium.com/max/544/1*TxrD3p6nwmryJPtyaOPdQw.png" alt="Logo" width="210" height="60">
     </a>
</div>
Khi xảy ra hiện tượng mất cân bằng, chúng ta muốn rằng mô hình sẽ dự báo chuẩn hơn đối với những class thiểu số. Do đó cần một hàm loss function hiệu quả hơn, có thể điều chỉnh được giá trị phạt lớn hơn nếu dự báo sai đối với nhóm thiểu số. Mục đích là để hạn chế dự báo sai nhóm thiểu số vì nếu dự báo sai nhóm thiểu số thì hàm loss function sẽ trở nên lớn hơn.
<div align="center">
     <a>
          <img src="https://miro.medium.com/max/426/1*P9-gyIKp1WjdolhiehwfFg.png" alt="Logo" width="210" height="60"> </br>
     </a>
</div>
Hàm balanced cross entropy là hàm số cân bằng được tỷ lệ phân phối của mẫu. Nhưng nó chưa thực sự thay đổi được gradient descent của loss function. Trong khi mô hình được huấn luyện trên mẫu mất cân bằng trầm trọng có giá trị gradient descent chịu ảnh hưởng phần lớn bởi class chiếm đa số.
<div align="center">
     <a>
          <img src="https://miro.medium.com/max/524/1*kJ_nhgNespK_SjD17d9qBA.png" alt="Logo" width="210" height="60"> </br>
     </a>
</div>
Ta thấy hàm focal loss chỉ thêm nhân tử (1-p<sub>t</sub>)<sup>y</sup> so với công thức của balanced cross entropy. Tuy nhiên nhân tử này lại có tác dụng rất lớn trong việc điều chỉnh ảnh hưởng của nhãn lên đồng thời loss function và gradient descent. </br>
<ins>Dễ dự báo:</ins> p<sub>t</sub> sẽ lớn do đó (1-p<sub>t</sub>)<sup>y</sup> có xu hướng rất nhỏ và dường như không tác động lên loss function và gradient descent đáng kể.</br>
<ins>Khó dự báo:</ins> p<sub>t</sub> sẽ nhỏ do đó (1-p<sub>t</sub>)<sup>y</sup> lớn tác động của nó lên loss function và gradient descent là sẽ gần bằng 1. Mức độ tác động này lớn hơn nhiều lần so với trường hợp dễ dự báo.

### Giới thiệu về FasterRCNN:
<h3>FasterRCNN:</h3>
*Faster R-CNN là mô hình tốt nhất của họ nhà R-CNN, được công bố đầu tiên vào năm 2015. </br>
*Được kế thừa từ Fast R-CNN. Tuy nhiên với việc thay thế thuật toán selective search bằng mạng Region Proposal Network. Nhờ đó Faster R-CNN nhanh hơn hẳn các dòng R-CNN trước đó.

### Giới thiệu về YOLOv5:

<p align="right">(<a href="#top">back to top</a>)</p>
