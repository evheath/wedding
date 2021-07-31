---
layout: default
---

# The venue
<!-- ![Venue1](/assets/img/venue1.JPG){:class="img-responsive"} -->

<!-- <img id="myimg"> -->

<!-- <script src="https://www.gstatic.com/firebasejs/8.8.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.8.1/firebase-storage.js"></script> -->
<script>
  // console.log("start");
  // var firebaseConfig = {
  //   apiKey: "AIzaSyA05ANqcrmkv-zGgo35y-mGyEwM42UkPlM",
  //   authDomain: "elliotandtina.firebaseapp.com",
  //   projectId: "elliotandtina",
  //   storageBucket: "elliotandtina.appspot.com",
  //   messagingSenderId: "1090811861387",
  //   appId: "1:1090811861387:web:e00d750cacf1002d7fb78e"
  // };
  // Initialize Firebase
  // firebase.initializeApp(firebaseConfig);
  var storage = firebase.storage();
  // var pathReference = storage.ref('venue/bridge1.JPG');
  // pathReference.getDownloadURL()
  //   .then((url) => {
  //     // console.log(url)
  //     // var img = document.getElementById('myimg');
  //     // img.setAttribute('src', url);
  //     var newImgElement = document.createElement('img');  //creating element
  //     newImgElement.setAttribute('class', "img-responsive");
  //     newImgElement.setAttribute('src', url);
  //     const section = document.getElementsByTagName("section")[0]; 
  //     // console.log(section)
  //     section.appendChild(newImgElement);           //appending the element
  //   }).catch((e) => {
  //     console.log(e)
  //   });
  venueRef = storage.ref('venue');
  // console.log(venueRef.listAll())
  venueRef.listAll()
  .then((res) => {
    // res.prefixes.forEach((folderRef) => {
    //   // All the prefixes under listRef.
    //   // You may call listAll() recursively on them.
    //   console.log(folderRef)
    // });
    res.items.forEach((itemRef) => {
      // All the items under listRef.
      // console.log(itemRef)
        itemRef.getDownloadURL()
          .then((url) => {
            // console.log(url)
            // var img = document.getElementById('myimg');
            // img.setAttribute('src', url);
            var newImgElement = document.createElement('img');  //creating element
            newImgElement.setAttribute('class', "img-responsive");
            newImgElement.setAttribute('src', url);
            const section = document.getElementsByTagName("section")[0]; 
            // console.log(section)
            section.appendChild(newImgElement);           //appending the element
          }).catch((e) => {
            console.log(e)
          });
    });
  }).catch((e) => {
    // Uh-oh, an error occurred!
    console.error(e)
  });
  // console.log("end")
</script>