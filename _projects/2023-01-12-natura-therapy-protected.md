<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="robots" content="noindex, nofollow">
    <title>Password Protected Page</title>
    <style>
        html, body {
            margin: 0;
            width: 100%;
            height: 100%;
            font-family: Arial, Helvetica, sans-serif;
        }
        #dialogText {
            color: white;
            background-color: #333333;
        }
        
        #dialogWrap {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: table;
            background-color: #EEEEEE;
        }
        
        #dialogWrapCell {
            display: table-cell;
            text-align: center;
            vertical-align: middle;
        }
        
        #mainDialog {
            max-width: 400px;
            margin: 5px;
            border: solid #AAAAAA 1px;
            border-radius: 10px;
            box-shadow: 3px 3px 5px 3px #AAAAAA;
            margin-left: auto;
            margin-right: auto;
            background-color: #FFFFFF;
            overflow: hidden;
            text-align: left;
        }
        #mainDialog > * {
            padding: 10px 30px;
        }
        #passArea {
            padding: 20px 30px;
            background-color: white;
        }
        #passArea > * {
            margin: 5px auto;
        }
        #pass {
            width: 100%;
            height: 40px;
            font-size: 30px;
        }
        
        #messageWrapper {
            float: left;
            vertical-align: middle;
            line-height: 30px;
        }
        
        .notifyText {
            display: none;
        }
        
        #invalidPass {
            color: red;
        }
        
        #success {
            color: green;
        }
        
        #submitPass {
            font-size: 20px;
            border-radius: 5px;
            background-color: #E7E7E7;
            border: solid gray 1px;
            float: right;
            cursor: pointer;
        }
        #contentFrame {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        #attribution {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            text-align: center;
            padding: 10px;
            font-weight: bold;
            font-size: 0.8em;
        }
        #attribution, #attribution a {
            color: #999;
        }
        .error {
            display: none;
            color: red;
        }
    </style>
  </head>
  <body>
    <iframe id="contentFrame" frameBorder="0" allowfullscreen></iframe>
    <div id="dialogWrap">
        <div id="dialogWrapCell">
            <div id="mainDialog">
                <div id="dialogText">This page is password protected.</div>
                <div id="passArea">
                    <p id="passwordPrompt">Password</p>
                    <input id="pass" type="password" name="pass" autofocus>
                    <div>
                        <span id="messageWrapper">
                            <span id="invalidPass" class="error">Sorry, please try again.</span>
                            <span id="trycatcherror" class="error">Sorry, something went wrong.</span>
                            <span id="success" class="notifyText">Success!</span>
                            &nbsp;
                        </span>
                        <button id="submitPass" type="button">Submit</button>
                        <div style="clear: both;"></div>
                    </div>
                </div>
                <div id="securecontext" class="error">
                    <p>
                        Sorry, but password protection only works over a secure connection. Please load this page via HTTPS.
                    </p>
                </div>
                <div id="nocrypto" class="error">
                    <p>
                        Your web browser appears to be outdated. Please visit this page using a modern browser.
                    </p>
                </div>
            </div>
        </div>
    </div>
    <div id="attribution">
        Protected by <a href="https://www.maxlaumeister.com/pagecrypt/">PageCrypt</a>
    </div>
    <script>
    (function() {

        var pl = "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";
        
        var submitPass = document.getElementById('submitPass');
        var passEl = document.getElementById('pass');
        var invalidPassEl = document.getElementById('invalidPass');
        var trycatcherror = document.getElementById('trycatcherror');
        var successEl = document.getElementById('success');
        var contentFrame = document.getElementById('contentFrame');
        
        // Sanity checks

        if (pl === "") {
            submitPass.disabled = true;
            passEl.disabled = true;
            alert("This page is meant to be used with the encryption tool. It doesn't work standalone.");
            return;
        }

        if (!isSecureContext) {
            document.querySelector("#passArea").style.display = "none";
            document.querySelector("#securecontext").style.display = "block";
            return;
        }

        if (!crypto.subtle) {
            document.querySelector("#passArea").style.display = "none";
            document.querySelector("#nocrypto").style.display = "block";
            return;
        }
        
        function str2ab(str) {
            var ustr = atob(str);
            var buf = new ArrayBuffer(ustr.length);
            var bufView = new Uint8Array(buf);
            for (var i=0, strLen=ustr.length; i < strLen; i++) {
                bufView[i] = ustr.charCodeAt(i);
            }
            return bufView;
        }

        async function deriveKey(salt, password) {
            const encoder = new TextEncoder()
            const baseKey = await crypto.subtle.importKey(
                'raw',
                encoder.encode(password),
                'PBKDF2',
                false,
                ['deriveKey'],
            )
            return await crypto.subtle.deriveKey(
                { name: 'PBKDF2', salt, iterations: 100000, hash: 'SHA-256' },
                baseKey,
                { name: 'AES-GCM', length: 256 },
                true,
                ['decrypt'],
            )
        }
        
        async function doSubmit(evt) {
            submitPass.disabled = true;
            passEl.disabled = true;

            let iv, ciphertext, key;
            
            try {
                var unencodedPl = str2ab(pl);

                const salt = unencodedPl.slice(0, 32)
                iv = unencodedPl.slice(32, 32 + 16)
                ciphertext = unencodedPl.slice(32 + 16)

                key = await deriveKey(salt, passEl.value);
            } catch (e) {
                trycatcherror.style.display = "inline";
                console.error(e);
                return;
            }

            try {
                const decryptedArray = new Uint8Array(
                    await crypto.subtle.decrypt({ name: 'AES-GCM', iv }, key, ciphertext)
                );

                let decrypted = new TextDecoder().decode(decryptedArray);

                if (decrypted === "") throw "No data returned";

                const basestr = '<base href="." target="_top">';
                const anchorfixstr = `
                    <script>
                        Array.from(document.links).forEach((anchor) => {
                            const href = anchor.getAttribute("href");
                            if (href.startsWith("#")) {
                                anchor.addEventListener("click", function(e) {
                                    e.preventDefault();
                                    const targetId = this.getAttribute("href").substring(1);
                                    const targetEl = document.getElementById(targetId);
                                    targetEl.scrollIntoView();
                                });
                            }
                        });
                    <\/script>
                `;
                
                // Set default iframe link targets to _top so all links break out of the iframe
                if (decrypted.includes("<head>")) decrypted = decrypted.replace("<head>", "<head>" + basestr);
                else if (decrypted.includes("<!DOCTYPE html>")) decrypted = decrypted.replace("<!DOCTYPE html>", "<!DOCTYPE html>" + basestr);
                else decrypted = basestr + decrypted;

                // Fix fragment links
                if (decrypted.includes("</body>")) decrypted = decrypted.replace("</body>", anchorfixstr + '</body>');
                else if (decrypted.includes("</html>")) decrypted = decrypted.replace("</html>", anchorfixstr + '</html>');
                else decrypted = decrypted + anchorfixstr;
                
                contentFrame.srcdoc = decrypted;
                
                successEl.style.display = "inline";
                setTimeout(function() {
                    dialogWrap.style.display = "none";
                }, 1000);
            } catch (e) {
                invalidPassEl.style.display = "inline";
                passEl.value = "";
                submitPass.disabled = false;
                passEl.disabled = false;
                console.error(e);
                return;
            }
        }
        
        submitPass.onclick = doSubmit;
        passEl.onkeypress = function(e){
            if (!e) e = window.event;
            var keyCode = e.keyCode || e.which;
            invalidPassEl.style.display = "none";
            if (keyCode == '13'){
              // Enter pressed
              doSubmit();
              return false;
            }
        }
    })();
    </script>
  </body>
</html>
