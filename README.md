# bg-remover
<!DOCTYPE html>
<html>
<head>
    <title>Alam's BG Remover</title>
    <style>
        body { text-align: center; font-family: Arial; padding: 20px; }
        input, button { padding: 10px; margin: 10px; }
        img { border: 2px solid #ddd; border-radius: 5px; }
    </style>
</head>
<body>
    <h1>🌄 Alam's Background Remover</h1>
    <input type="file" id="imageInput" accept="image/*">
    <button onclick="removeBackground()">बैकग्राउंड हटाएं</button>
    <div id="result"></div>

    <script>
        async function removeBackground() {
            const apiKey = 'YOUR_API_KEY'; // XcM6esmhiPpWtfATnNURVHGK
            const imageInput = document.getElementById('imageInput');
            
            const formData = new FormData();
            formData.append('image_file', imageInput.files[0]);

            try {
                const response = await fetch('https://api.remove.bg/v1.0/removebg', {
                    method: 'POST',
                    headers: { 'X-Api-Key': apiKey },
                    body: formData
                });

                if (!response.ok) {
                    throw new Error('Remove.bg API failed');
                }

                const blob = await response.blob();
                const resultUrl = URL.createObjectURL(blob);
                
                document.getElementById('result').innerHTML = `
                    <h3>✅ बैकग्राउंड रिमूव्ड!</h3>
                    <img src="${resultUrl}" style="max-width: 500px;">
                    <br><a href="${resultUrl}" download="no-bg.png" style="display: block; margin-top: 10px;">
                        <button>डाउनलोड करें</button>
                    </a>
                `;
            } catch (error) {
                alert('❌ कुछ गलत हुआ! API Key चेक करें या इमेज फिर से अपलोड करें।');
            }
        }
    </script>
</body>
</html>
