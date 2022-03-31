<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">

    <title>To Do's List</title>
  </head>
  <body>
      <!--navigation bar-->
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">To Do's List</a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="#">Home</a>
              </li>
            </ul>
            <form class="d-flex">
              <button class="btn btn-outline-warning" type="submit">Here you can create your list</button>
            </form>
          </div>
        </div>
      </nav>
      <div class="container">
          <h2 class="text-center">To Do's list</h2>
            <div class="form-group">
              <label for="Title" class="form-label">Title</label>
              <input type="text" class="form-control" id="title" aria-describedby="emailHelp">
              <div id="emailHelp" class="form-text text-muted">In above section you can add item on list</div>
            </div>
            <div class="form-group my-4">
                <label for="description" >Description</label>
                <textarea class="form-control" id="description" rows="3"></textarea>
                <div id="emailHelp" class="form-text text-muted">In this section you can add item description on list</div>
              </div>

            <button class="btn btn-warning" id="add" >Add item on list</button>
            <button class="btn btn-danger" id="clear" onclick="clearStorage()">Clear list</button>

            <div id="items"class="my-4">
                <h2>All Your Items</h2>
                <table class="table">
                    <thead>
                      <tr>
                        <th scope="col">S.no.</th>
                        <th scope="col">Title</th>
                        <th scope="col">Description </th>
                        <th scope="col">Actions</th>
                      </tr>
                    </thead>
                    <tbody id="tableBody">
                      <tr>
                        <th scope="row">1</th>
                        <td>Get Some Coffee</td>
                        <td>You need a coffee aas you are a coder</td>
                        <td><button class="btn btn-sm btn-primary">Delete</button></td>
                      </tr>
                      <tr>
                    </tbody>
                  </table>
            </div>

      </div>

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.10.2/dist/umd/popper.min.js" integrity="sha384-7+zCNj/IqJ95wo16oMtfsKbZ9ccEh31eOz1HGyDuCQ6wgnyJNSYdrPa03rtR1zdB" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.min.js" integrity="sha384-QJHtvGhmr9XOIpI6YVutG+2QOK9T+ZnN4kzFN1RtK3zEFEIsxhlmWl5/YESvpZ13" crossorigin="anonymous"></script>
    -->
    <script>
        function getAndUpdate(){
            console.log("Updating list...");
            tit = document.getElementById('title').value;
            desc = document.getElementById('description').value;
            if (localStorage.getItem('itemsjson')==null){
                itemJsonArray = [];
                itemJsonArray.push([tit, desc]);
                localStorage.setItem('itemsJson',JSON.stringify(itemJsonArray))
            }
            else{
                itemJsonArrayStr = localStorage.getItem('itemsJson')
                itemJsonArray = JSON.parse(itemJsonArrayStr);
                itemJsonArray.push([tit, desc]);
                localStorage.setItem('itemsjson', JSON.stringify(itemJsonArray))
            }
            Update();
        }
        function Update(){
            if(localStorage.getItem('itemsJson')==null){
                itemJsonArray = [];
                localStorage.setItem('itemsJson',JSON.stringify(itemJsonArray))
            }
            else{
                itemJsonArrayStr = localStorage.getItem('itemsJson')
                itemJsonArray = JSON.parse(itemJsonArrayStr);
            }
            //populate the table
            let tableBody = document.getElementById("tableBody");
            let str = "";
            itemJsonArray.forEach((element, index) => {
                str += `
                <tr>
                        <th scope="row">${index + 1}</th>
                        <td>${element[0]}</td>
                        <td>${element[1]}</td>
                        <td><button class="btn btn-sm btn-primary" onclick="deleted(${index})">Delete</button></td>
                      </tr> `;
            });
            tableBody.innerHTML = str;
        }
        add = document.getElementById("add");
        add.addEventListener("click",getAndUpdate)

        function deleted(itemindex){
            console.log("Delete",itemindex);
            itemJsonArrayStr = localStorage.getItem('itemsJson')
            itemJsonArray = JSON.parse(itemJsonArrayStr);
            // Delete itemindex elementy from the array
            itemJsonArray.splice(itemindex, 1);
            localStorage.setItem('itemsJson', JSON.stringify(itemJsonArray));
            Update();

        }
        function clearStorage(){
            if (confirm("Do you really want to delete to clear?")){
                console.log('clearing the storage')
                localStorage.clear();
                Update();
            }
        }
    </script>
  </body>
</html>
