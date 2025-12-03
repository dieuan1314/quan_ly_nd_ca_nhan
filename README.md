# quan_ly_nd_ca_nhan
WEBSITE QUẢN LÝ NỘI DUNG CÁ NHÂN
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CHức năng của user</title>
</head>
<style>
body {
  font-family: Arial, sans-serif;
  background-color:rgb(103, 190, 240);
  color: #012549;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  background-color: #ffffff;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 51, 102, 0.2);
  width: 300px;
}

h1, h2,h3 {
  text-align: center;
  color: #0055cc;
}

input, select, button {
  width: 100%;
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #0055cc;
  border-radius: 5px;
}

button {
  background-color: #0055cc;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #003366;
}
textarea {
    width: 100%;
    height:60px;
    padding:10px;
    border-radius: 10px;
    border:1px solid rgb(82, 57, 184);

}
</style>
<body>
  <div  id="manage">
    <h2>Quản Lý nội dung</h2>
    <form id="addcontent">
        <input type="text" id="title" placeholder="Tiêu đề" required>
        <input type="text" id="topic" placeholder="Chủ đề"  required>
        <textarea id="description" placeholder="Mô tả ngắn " required></textarea>
        <select id="choice">
            <option >Công khai</option>
            <option>Riêng tư</option>
        </select>
        <button type="submit">Thêm nội dung</button>

    </form>
    <h3>Bài đăng của bạn </h3>
    <h4>Bài đăng riêng tư</h4>
    <div id="yourshelfprivatecontent"></div>
    <h4>Bài đăng công khai </h4>
    <div id="yourshelfpubliccontent"></div>

    <h3>Bài đăng của người khác </h3>
    <div id="themselvescontent"></div>

  </div>

  <script>
    let currentUser=null;
 
document.getElementById("manage").addEventListener("submit",function(e){
    e.preventDefault();
    const title=document.getElementById("title").value;
    const topic=document.getElementById("topic").value;
    const description=document.geElementById("description").value;
    const choice=documnet.getElement("choice").value;
    const contents=JSON.parse(localStorage.getItem("contents"))||[];
    contents.push({
        username: currentUser.username,
        title,
        topic,
        description,
        choice,
        create: new Date().toISOString()

    });
    localStorage.setItem("contents",JSON.stringify(contents));
    loadContents();


});
function loadContents(){
    const contents = JSON.parse(localStoge.getItem("contents"))||[];
    const yourshelfprivatecontent=contents.filter(c=>c.username===currentUser.username && c.choice==="riêng tư");
    const yourshelfpubliccontent=contents.filter(c=>c.username===currentUser&&c.choice==="công khai")
    const themshelvescontent=contents.filter(c=>c.username!==currentUser.username && c.choice==="công khai" );
    
    document.getElementById("yourshelfprivatecontent").innerHTML="";
    document.getElementById("yourshelfpubliccontent").innerHTML="";
    document.getElementById("themshelvescontent").innerHTML="";
    
yourshelfprivatecontent.forEach(c=>{
    yourshelfprivatecontent.innerHTML+=`
    <div class="content-item">
        <strong>${c.title}</strong><br/>
        Chủ đề: ${c.topic}<br/>
        Mô tả ngắn: ${c.description}<br/>
        Trạng thái: ${c.choice}<br/>
        Ngày tạo: ${new Date(c.create).toLocalstring()}
        </div>`;
})
yourshelfpubliccontent.forEach(c=>{
    yourshelfpubliccontent.innerHTML+=`
    <div class="content-item">
        <strong>${c.title}</strong><br/>
        Chủ đề: ${c.topic}<br/>
        Mô tả ngắn: ${c.description}<br/>
        Trạng thái: ${c.choice}<br/>
        Ngày tạo: ${new Date(c.create).toLocalstring()}
        </div>`;
})
themshelvescontent.forEach(c=>{
    themshelvescontent.innerHTML+=`
    <div class="content-item">
        <strong>${c.title}</strong><br/>
        Chủ đề: ${c.topic}<br/>
        Mô tả ngắn: ${c.description}<br/>
        Trạng thái: ${c.choice}<br/>
        Ngày tạo: ${new Date(c.create).toLocalstring()}
        </div>`;
})

 function toggleSection(id){
    const secsion=document.getElementById(id);
    section.style.display=section.style.display==="block"?"none":"block";
 }

  </script>
</body>
</html>
    
    
