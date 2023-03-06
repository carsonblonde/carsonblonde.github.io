---
layout: post
title:  "Estimating Pi With Monte Carlo Method"
---



<canvas id="monte" width="700" height="480"></canvas>

<script>
    const canvas = document.getElementById("monte");
    const ctx = canvas.getContext("2d");
    const rad = 240;

    let x = 0;
    let y = 0;

    let total = 0;
    let inCircle = 0;

    function reset() {
        ctx.beginPath();
        ctx.rect(rad*2,0,rad,rad*2);
        ctx.fillStyle = "white";
        ctx.fill()
        ctx.closePath();
    }

    function drawText() {
        ctx.beginPath();
        ctx.font = "20px arial";
        ctx.fillStyle = "black";
        ctx.fill()
        ctx.fillText("Total: " + total, rad*2+10, 30);
        ctx.fillText("In Circle: " + inCircle, rad*2+10, 60);
        ctx.fillText("Estimation: " + (4*inCircle/total).toFixed(4), rad*2+10, 90);
        ctx.closePath();
    }

    function checkCircle(x, y, r) {
        if(r >= Math.sqrt(Math.pow(x-r,2)+Math.pow(y-r,2))) {
            return true
        } else {
            return false
        }
    }

    function drawPoint(x, y, colour) {
        ctx.beginPath();
        ctx.arc(x,y,2,0,Math.PI*2);
        ctx.fillStyle = colour;
        ctx.fill();
        ctx.closePath();
    }

    function drawCircle() {
        ctx.beginPath();
        ctx.arc(rad,rad,rad-1,0,Math.PI*2);
        ctx.lineWidth = 1;
        ctx.strokeStyle = 'black';
        ctx.stroke();
        ctx.closePath();
    }

    function draw() {
        drawCircle();
        x = Math.floor(Math.random()*(rad*2+1))
        y = Math.floor(Math.random()*(rad*2+1))
        
        total += 1;
        if(checkCircle(x, y, rad)) {
            inCircle += 1;
            drawPoint(x, y, "red");
        } else {
            drawPoint(x, y, "blue"); 
        }
        reset();
        drawText();
    }

    setInterval(draw, 0.1);
</script>