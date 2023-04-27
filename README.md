# ASSIGNMENT-6
starting with the code handout please make sure that the clock works correctly for each selected timezone from the dropdown.

<!doctype html>
<html>

<head>
    <style>
        body {
            margin: 0;
        }
        
        #container {
            width: 100vw;
            height: 100vh;
        }
        
        .slide {
            width: 100%;
            height: 100%;
            background-repeat: no-repeat;
            background-position: 50% 50%;
            display: block;
            position: absolute;
            transition: 2s;
        }
        
        #prev {
            position: fixed;
            bottom: 10px;
            left: 10px;
        }
        
        #next {
            position: fixed;
            bottom: 10px;
            right: 10px;
        }
        
        #numContainer {
            position: fixed;
            width: 60%;
            left: 20%;
            text-align: center;
            bottom: 10px;
        }
        
        .active {
            background: gold;
        }
    </style>
    <script>
        var allImages = [];
        var currentSlide = 0;
        var aniType = "fading";

        function start() {
            var hash = window.location.hash.replace("#", "");
            allImages = hash.split(",");
            if (allImages[allImages.length] == "sliding") {
                aniType = "sliding";
            }
            allImages.pop();
            var markup = "";
            for (var i = 0; i < allImages.length; i++) {
                markup += "<div class='slide' style='background-image:url(" + allImages[i] + ")'></div>"
            }
            document.getElementById("container").innerHTML = markup;
            markup = "";
            for (var i = 0; i < allImages.length; i++) {
                markup += "<button onclick='numClicked(" + i + ")' class='num'>" + (i + 1) + "</button>"
            }
            document.getElementById("numContainer").innerHTML = markup;
            if (aniType == "fading") {
                document.getElementsByClassName("slide")[0].style.opacity = 1;
            } else {
                document.getElementsByClassName("slide")[0].style.left = 0;
            }
            goToCurrentSlide();
        }
        var goPrev = function() {
            currentSlide = currentSlide - 1
            if (currentSlide < 0) {
                currentSlide = allImages.length;
            }
            goToCurrentSlide();
        }
        var goNext = function() {
            currentSlide = currentSlide + 1;
            if (currentSlide >= allImages.length) {
                currentSlide = 0;
            }
            goToCurrentSlide();
        }
        var numClicked = function(n) {
            currentSlide = n;
            goToCurrentSlide();
        }
        var goToCurrentSlide = function() {
            if (aniType == "fading") {
                for (var i = 0; i < allImages.length; i++) {
                    document.getElementsByClassName("slide")[i].style.opacity = 0;
                }
                document.getElementsByClassName("slide")[currentSlide].style.opacity = 1;
            } else {
                for (var i = 0; i < allImages.length; i++) {
                    document.getElementsByClassName("slide")[i].style.left = "100%";
                }
                document.getElementsByClassName("slide")[currentSlide].style.left = 0;
            }
        }
    </script>
</head>

<body onload='start()'>
    <div id='container'>
    </div>
    <div id='numContainer'>
    </div>
    <button onclick='goPrev()' id='prev'> Prev </button>
    <button onclick='goNext()' id='next'> Next </button>
</body>

</html>

</html>
