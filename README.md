 /////                                  //      linked list of singular
 
public class implentation {

    public static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
        }
    }

    public static class LinkedList {
        Node head = null;
        Node tail = null;
        void insertAtBegin(int val) {
            Node temp = new Node(val);

            if (head == null) {
                // empty list
                head = temp;
                tail = temp;
            } else {
                // non-empty list
                temp.next = head;
                head = temp;
            }
        }
            // create the function to add at the list
            void insertAtEnd(int val) {
                // create the node which want to add ;
                Node temp = new Node(val);
    
                // if our list is empty
                if (head == null) {
                    head = temp;
                    tail = temp;
                } else {
                    tail.next = temp;
                    tail = temp;
                }
            }

        void insertMiddle(int idx, int val) {
            Node t = new Node(val);
            Node temp = head;

            if (idx == length()) {
                insertAtEnd(val);
                return;
            } else if (idx == 0) {
                insertAtBegin(val);
                return;
            } else if (idx < 0 || idx > length()) {
                System.out.println("wrong index");
                return;
            }

            for (int i = 0; i < idx - 1; i++) {
                temp = temp.next;
            }
            t.next = temp.next;
            temp.next = t;
        }

        // to get the element

        int getAt(int idx) { 
            Node temp = head;
            for (int i = 0; i < idx; i++) {
                temp = temp.next;
            }
            return temp.data;
        }

        void delete(int idx) {
            if(idx == 0){
                head = head.next;
                return;
            }
            Node temp = head;
           
            for (int i = 0; i < idx - 1; i++) {
                temp = temp.next;
                
            }
            temp.next = temp.next.next;
            tail = temp ; // for the point at last like ll.tail.data
        }

        void display() {
            Node temp = head;
            while (temp != null) {
                System.out.print(temp.data + " ");
                temp = temp.next;
            }
        }

        int length() {
            int count = 0;
            Node temp = head; // use a local variable instead of modifying head
            while (temp != null) {
                count++;
                temp = temp.next;
            }
            return count;
        }

    }

    public static void main(String[] args) {
        LinkedList ll = new LinkedList();

        ll.insertAtEnd(15);
        ll.insertAtBegin(78);
        ll.insertAtEnd(100);
        ll.insertMiddle(2, 10);
        ll.insertMiddle(3, 22);
        ll.insertMiddle(0, 1);
        // / ll.insertMiddle(-1, 224); //wrong index
        // ll.delete(2);
        // ll.delete(4);
        ll.delete(0);
        ll.display();

        System.out.println();
        System.out.println(ll.length());
        // System.out.println(ll.getAt(0)); // to get value
        // System.out.println(ll.getAt(3)); // to get value

        System.out.println(ll.tail.data);

    }
}




                                        ////  Xml faetch daata from the table as view 





                <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Item Menu Page</title>
    <link rel="stylesheet" href="/Resturant website/Styling/itemMenu.css" />
    <script src="/jquery-3.7.1.min.js"></script>
  </head>
  <body>
    <main>
      <section>
        <header class="header">
          <div>
            <h1>Resturant</h1>
          </div>
          <div>
            <ul class="list">
              <a href="/Resturant website/Html/Home.html"><li>Home</li></a>
              <a href="/Resturant website/Html/about.html"> <li>About</li></a>
              <a href="/Resturant website/Html/contact.html">
                <li>Contact</li></a
              >
              <a href="/Resturant website/Html/find.html"> <li>Search</li></a>

              <a href="/Resturant website/Html/itemMenu.html"
                ><li>Item Menu</li></a
              >

              <a href="/Resturant website/Html/profile.html">
                <li>Profile</li></a
              >

              <a href="/Resturant website/Html/login.html"> <li>Login</li></a>
              <a href="/Resturant website/Html/xmlFile.htm"> <li>XML</li></a>
            </ul>
          </div>
        </header>
      </section>
      <section>
        <button id="show">Show</button>
        <button id="hide">Hide</button>
        <div>
          <table>
            <thead class="thead">
              <tr>
                <th>Menu Id</th>
                <th>Food Category</th>
                <th>Food Item Name</th>
                <th>Food Ingredients</th>
                <th>Price</th>
                <th>Qty</th>
              </tr>
            </thead>
            <tbody id="tbody"></tbody>
          </table>
        </div>
      </section>
    </main>
  </body>
  <script>
    // function to fetch data from json :
    function fetchData() {
      // declare the httprequest :
      let xhttp = new XMLHttpRequest();

      xhttp.onreadystatechange = function () {
        if (xhttp.readyState == XMLHttpRequest.DONE && xhttp.status == 200) {
          let data = JSON.parse(xhttp.responseText);
          render(data);
        }
      };

      xhttp.open("GET", "/Resturant website/data/info.json", true);
      xhttp.send();
    }
    
    // function to help display json data to webapge ;

    function render(data) {
      let tbody = document.querySelector("#tbody");

      tbody.innerHTML = "";

      data.forEach((element) => {

        console.log(element);

        let tr = document.createElement("tr");
        let ul = document.createElement("ul");
        
        element.foodIngredients.forEach((el) => {
          let li = document.createElement("li");
          li.textContent = el;
          ul.appendChild(li);
        });

        tr.innerHTML = `
               <td>${element.menuId}</td>
                <td>${element.foodCategory}</td>
                
                <td>${element.foodItemName}</td>
                <td id = "tddd"></td>
                <td>$${element.price}</td>
                <td>${element.qty}</td>
        `;

        tr.querySelector("td:nth-child(4)").appendChild(ul);
        tbody.appendChild(tr);
      });

      console.log(data);
    }

    document.getElementById("show").addEventListener("click", function () {
      fetchData();
      $("#tbody").show(1000);
    });
    document.getElementById("hide").addEventListener("click", function () {
      $("#tbody").hide(2000);
    });
  </script>
</html>



                           ///// featch data from the search  




    <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Find dishes</title>
    <link rel="stylesheet" href="/Resturant website/Styling/find.css" />
    <script src="/jquery-3.7.1.min.js"></script>
  </head>
  <body>
    <main>
      <section>
        <header class="header">
          <div>
            <h1>Resturant</h1>
          </div>
          <div>
            <ul class="list">
              <a href="/Resturant website/Html/Home.html"><li>Home</li></a>
              <a href="/Resturant website/Html/about.html"> <li>About</li></a>
              <a href="/Resturant website/Html/contact.html">
                <li>Contact</li></a
              >
              <a href="/Resturant website/Html/find.html"> <li>Search</li></a>

              <a href="/Resturant website/Html/itemMenu.html"
                ><li>Item Menu</li></a
              >

              <a href="/Resturant website/Html/profile.html">
                <li>Profile</li></a
              >

              <a href="/Resturant website/Html/login.html"> <li>Login</li></a>
              <a href="/Resturant website/Html/xmlFile.htm"> <li>XML</li></a>
            </ul>
          </div>
        </header>
      </section>
      <section>
        <div id="searching">
          <input
            type="text"
            id="inputSearch"
            placeholder="serach any dishes..."
          />
          <button id="searchBtn" onclick="fetchMenuData()">Search</button>
        </div>
        <div>
          <table>
            <thead class="thead">
              <tr>
                <th>Menu Id</th>
                <th>Food Category</th>
                <th>Food Item Name</th>
                <th>Food Ingredients</th>
                <th>Price</th>
                <th>Qty</th>
              </tr>
            </thead>
            <tbody id="tbody">


              
            </tbody>
          </table>
        </div>
      </section>
    </main>
  </body>

  <script>
    //   using ajax to call api or json data using javascript :
    function fetchMenuData() {
      const xhr = new XMLHttpRequest();
      xhr.onreadystatechange = function () {
        if (xhr.readyState == XMLHttpRequest.DONE) {
          if (xhr.status == 200) {
            let data = JSON.parse(xhr.responseText);
            // console.log(data);
            render(data);
          }
        }
      };
      xhr.open("GET", "/Resturant website/data/info.json", true);
      xhr.send();
    }

    function render(data) {
      const value = document.querySelector("#inputSearch").value;

      let tbody = document.querySelector("#tbody");
      tbody.innerHTML = "";
      data.forEach((element) => {
        if (element.foodItemName.toLowerCase().startsWith(value)) {
          const tr = document.createElement("tr");
          const tdIngredients = document.createElement("td");
          const ul = document.createElement("ul");

          element.foodIngredients.forEach((ingredient) => {
            const li = document.createElement("li");
            li.textContent = ingredient;
            ul.appendChild(li);
          });

          tr.innerHTML = `
            <td>${element.menuId}</td>
            <td>${element.foodCategory}</td>
            <td>${element.foodItemName}</td>
            <td></td> <!-- Placeholder for ingredients -->
            <td>$${element.price}</td>
            <td>${element.qty}</td>
        `;

          // Append the list of ingredients to the corresponding table cell
          tdIngredients.appendChild(ul);
          tr.querySelector("td:nth-child(4)").appendChild(ul);
          tbody.appendChild(tr);
        }
      });
      //   document.querySelector("#inputSearch").value = "";
      $("#tbody").show(3000);
    }

    // using ajax to call api or json data using jquery :
  </script>
</html>

