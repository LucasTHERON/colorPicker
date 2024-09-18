<script>

    //COLORS

    let currentColor = $state({r:0,g:0,b:0});

    let complementaryColor = $derived({
        r: 255 - currentColor.r,
        g: 255 - currentColor.g,
        b: 255 - currentColor.b,
    });

    let dividedColorBy2 = $derived({
        r: (currentColor.r / 2) < 1 ? 0 : Math.floor(currentColor.r / 2),
        g: (currentColor.g / 2) < 1 ? 0 : Math.floor(currentColor.g / 2),
        b: (currentColor.b / 2) < 1 ? 0 : Math.floor(currentColor.b / 2),
    });

    let dividedCompBy2 = $derived({
        r: (complementaryColor.r / 2) < 1 ? 0 : Math.floor(complementaryColor.r / 2),
        g: (complementaryColor.g / 2) < 1 ? 0 : Math.floor(complementaryColor.g / 2),
        b: (complementaryColor.b / 2) < 1 ? 0 : Math.floor(complementaryColor.b / 2),
    });

    let multiliedCompBy2 = $derived({
        r: (complementaryColor.r * 2) > 255 ? 255 : Math.floor(complementaryColor.r * 2),
        g: (complementaryColor.g * 2) > 255 ? 255 : Math.floor(complementaryColor.g * 2),
        b: (complementaryColor.b * 2) > 255 ? 255 : Math.floor(complementaryColor.b * 2),
    });

    let multiliedColorBy2 = $derived({
        r: (currentColor.r * 2) > 255 ? 255 : Math.floor(currentColor.r * 2),
        g: (currentColor.g * 2) > 255 ? 255 : Math.floor(currentColor.g * 2),
        b: (currentColor.b * 2) > 255 ? 255 : Math.floor(currentColor.b * 2),
    });

    let mixedRGColor = $derived({
        r: currentColor.g,
        g: currentColor.r,
        b: currentColor.b,
    });

    let mixedGBColor = $derived({
        r: currentColor.r,
        g: currentColor.b,
        b: currentColor.g,
    });

    let mixedRBColor = $derived({
        r: currentColor.b,
        g: currentColor.g,
        b: currentColor.r,
    });

    let dividedColorBy3 = $derived({
        r: (currentColor.r / 3) < 1 ? 0 : Math.floor(currentColor.r / 3),
        g: (currentColor.g / 3) < 1 ? 0 : Math.floor(currentColor.g / 3),
        b: (currentColor.b / 3) < 1 ? 0 : Math.floor(currentColor.b / 3),
    });

    let multiliedColorBy3 = $derived({
        r: (currentColor.r * 3) > 255 ? 255 : Math.floor(currentColor.r * 3),
        g: (currentColor.g * 3) > 255 ? 255 : Math.floor(currentColor.g * 3),
        b: (currentColor.b * 3) > 255 ? 255 : Math.floor(currentColor.b * 3),
    });

    function updateFromPicker(hex){

        let rgbR = parseInt(hex.substring(1, 3), 16);
        let rgbG = parseInt(hex.substring(3, 5), 16);
        let rgbB = parseInt(hex.substring(5, 7), 16);

        currentColor = {
            r: rgbR,
            g: rgbG,
            b: rgbB,
        }
        
        
    }

    //CONVERT COLORS TO STRINGS

    function getRgbStr(color){
        return "rgb(" + color.r + "," + color.g + "," + color.b + ")";
    }

    function getHexStr(color){
        let hexR = color.r.toString(16);
        if (hexR.length == 1){ hexR = "0" + hexR; }
        let hexG = color.g.toString(16);
        if (hexG.length == 1){ hexG = "0" + hexG; }
        let hexB = color.b.toString(16);
        if (hexB.length == 1){ hexB = "0" + hexB; }
        return ("#" + hexR + hexG + hexB).toUpperCase();
    }

    function randomizeColor(e){
        console.log(e);

        if (e.key === " "){
           let newColor = {
                r: Math.floor(Math.random() * 255),
                g: Math.floor(Math.random() * 255),
                b: Math.floor(Math.random() * 255),
            }
            currentColor = newColor; 
        }
        
    }

    function convertRgbToHex(rgb) {
        console.log("r = " + rgb.r);
        console.log("g = " + rgb.g);
        console.log("b = " + rgb.b);
        let hexR = rgb.r.toString(16);
        if (hexR.length == 1){
            hexR = "0" + hexR;
        }
        let hexG = rgb.g.toString(16);
        if (hexG.length == 1){
            hexG = "0" + hexG;
        }
        let hexB = rgb.b.toString(16);
        if (hexB.length == 1){
            hexB = "0" + hexB;
        }
        
    }

    randomizeColor({key : " "});

    function consolelogthat(){
        console.log("onchange");
        
    }

</script>
<svelte:window
    onkeydown={(e) => randomizeColor(e)}
/>
<h1>My color : { getRgbStr(currentColor) } / { getHexStr(currentColor) }</h1>
<div style="background: { getRgbStr(currentColor) }, height: 50px; width: 50px"></div>




<div class="picker-container">
    <div class="color-picker">
        <input type="color" class="input" value="{ getHexStr(currentColor) }" onchange={(e) => updateFromPicker(e.target.value)}>
    </div>


    <div class="palette-section">
        <div class="palette-container">
            <h2>Complementary</h2>
            <div class="color-palette">
                <div style="background-color: { getRgbStr(currentColor) };">
                    <p>{ getRgbStr(currentColor) } / { getHexStr(currentColor) }</p>
                </div>
                <div style="background-color: { getRgbStr(dividedColorBy2) };">
                    <p>{ getRgbStr(dividedColorBy2) } / { getHexStr(dividedColorBy2) }</p>
                </div>
                <div style="background-color: { getRgbStr(multiliedColorBy2) };">
                    <p>{ getRgbStr(multiliedColorBy2) } / { getHexStr(multiliedColorBy2) }</p>
                </div>
                <div style="background-color: { getRgbStr(complementaryColor) };">
                    <p>{ getRgbStr(complementaryColor) } / { getHexStr(complementaryColor) }</p>
                </div>
                <div style="background-color: { getRgbStr(dividedCompBy2) };">
                    <p>{ getRgbStr(dividedCompBy2) } / { getHexStr(dividedCompBy2) }</p>
                </div>
                <div style="background-color: { getRgbStr(multiliedCompBy2) };">
                    <p>{ getRgbStr(multiliedColorBy2) } / { getHexStr(multiliedColorBy2) }</p>
                </div>
            </div>
        </div>

        <div class="palette-container">

            <h2>Shades</h2>
            <div class="color-palette">
                <div style="background-color: { getRgbStr(currentColor) };">
                    <p>{ getRgbStr(currentColor) } / { getHexStr(currentColor) }</p>
                </div>
                <div style="background-color: { getRgbStr(dividedColorBy2) };">
                    <p>{ getRgbStr(dividedColorBy2) } / { getHexStr(dividedColorBy2) }</p>
                </div>
                <div style="background-color: { getRgbStr(dividedColorBy3) };">
                    <p>{ getRgbStr(dividedColorBy3) } / { getHexStr(dividedColorBy3) }</p>
                </div>
                <div style="background-color: { getRgbStr(multiliedColorBy2) };">
                    <p>{ getRgbStr(multiliedColorBy2) } / { getHexStr(multiliedColorBy2) }</p>
                </div>
                <div style="background-color: { getRgbStr(multiliedColorBy3) };">
                    <p>{ getRgbStr(multiliedColorBy3) } / { getHexStr(multiliedColorBy3) }</p>
                </div>
            </div>
        </div>

        <div class="palette-container">
            <h2>Mixed</h2>  
            <div class="color-palette">
                <div style="background-color: { getRgbStr(currentColor) };">
                    <p>{ getRgbStr(currentColor) } / { getHexStr(currentColor) }</p>
                </div>
                <div style="background-color: { getRgbStr(mixedRGColor) };">
                    <p>{ getRgbStr(mixedRGColor) } / { getHexStr(mixedRGColor) }</p>
                </div>
                <div style="background-color: { getRgbStr(mixedGBColor) };">
                    <p>{ getRgbStr(mixedGBColor) } / { getHexStr(mixedGBColor) }</p>
                </div>
                <div style="background-color: { getRgbStr(mixedRBColor) };">
                    <p>{ getRgbStr(mixedRBColor) } / { getHexStr(mixedRBColor) }</p>
                </div>
            </div>
        </div>

    </div>

</div>


