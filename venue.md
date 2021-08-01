---
layout: default
---

# The venue

The wedding is taking place on 66-acre plot of private property in Mauston, Wisconsin. Affectionately known as 'Hamm Land' the property has passed through generations of Hamms who have taken care of the land by planting trees, maintaining trails, and--most notably--digging an artificial lake. Common sights around the property include familes of geese (with their fuzzy, little goslings), a myriad of small and large birds, and deer.

The lake makes connections with the Wisconsin River, has several small islands, and is home to several types of fish. 

<button disable='true' id="left">left</button>
<button id="right">right</button>

<div class="sk-fading-circle" id="loadingIndicator">
  <div class="sk-circle1 sk-circle"></div>
  <div class="sk-circle2 sk-circle"></div>
  <div class="sk-circle3 sk-circle"></div>
  <div class="sk-circle4 sk-circle"></div>
  <div class="sk-circle5 sk-circle"></div>
  <div class="sk-circle6 sk-circle"></div>
  <div class="sk-circle7 sk-circle"></div>
  <div class="sk-circle8 sk-circle"></div>
  <div class="sk-circle9 sk-circle"></div>
  <div class="sk-circle10 sk-circle"></div>
  <div class="sk-circle11 sk-circle"></div>
  <div class="sk-circle12 sk-circle"></div>
</div>

<img id="venueImage">

<script>
  // listener for image/loading-indicator
  $('#venueImage').on('load', function(){
    $('#loadingIndicator').hide();
    $('#venueImage').show();
  });

  var currentImageNum = 0
  var maxImageNum = 36
  var storage = firebase.storage();
  var allStorageRefs;

  //whenever a new image should be displayed
  function updateImage() {
      $('#loadingIndicator').show();
      $('#venueImage').hide();
      allStorageRefs[currentImageNum].getDownloadURL()
      .then((url) => {
        $('#venueImage').attr('src',url);
      })
  }

  //button handlers
  document.getElementById("right").addEventListener("click", () => {
    if (currentImageNum < maxImageNum) {
      currentImageNum+=1
      updateImage()
    }
  });
  document.getElementById("left").addEventListener("click", () => {
    if (currentImageNum > 0) {
      currentImageNum-=1
      updateImage()
    }
  });

  // getting all the refs
  storage.ref('venue').listAll()
  .then((res) => {
    // res.prefixes.forEach((folderRef) => {
    //   // All the prefixes under listRef.
    //   // You may call listAll() recursively on them.
    //   console.log(folderRef)
    // });
    allStorageRefs = res.items
    maxImageNum = allStorageRefs.length
    updateImage();
    // res.items.forEach((itemRef) => {
    //   // All the items under listRef.
    //   // console.log(itemRef)
    //     itemRef.getDownloadURL()
    //       .then((url) => {
    //         // console.log(url)
    //         // var img = document.getElementById('myimg');
    //         // img.setAttribute('src', url);
    //         var newImgElement = document.createElement('img');  //creating element
    //         newImgElement.setAttribute('class', "img-responsive");
    //         newImgElement.setAttribute('src', url);
    //         const section = document.getElementsByTagName("section")[0]; 
    //         // console.log(section)
    //         section.appendChild(newImgElement);           //appending the element
    //       }).catch((e) => {
    //         console.log(e)
    //       });
    // });
  }).catch((e) => {
    console.error(e)
  });
  // console.log("end")
</script>