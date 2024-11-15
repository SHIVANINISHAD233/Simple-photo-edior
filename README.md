# Simple-photo-edior
This photo editor lets users upload an image and apply dynamic filters like brightness, contrast, grayscale, and more in real-time. It features a responsive design and live preview, offering a seamless and interactive editing experience.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enhanced Photo Editor</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #f3f4f7, #dcdde1);
            color: #333;
        }

        .editor {
            background-color: #fff;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        h1 {
            font-size: 2rem;
            margin-bottom: 20px;
            color: #4b6584;
        }

        .filters {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
            margin-top: 20px;
        }

        .filter-option {
            flex: 1 1 calc(33% - 20px);
            min-width: 150px;
            max-width: 200px;
            background: #f9f9f9;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .filter-option:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #57606f;
        }

        select, input[type="file"] {
            width: 100%;
            padding: 8px 10px;
            border-radius: 5px;
            border: 1px solid #dcdde1;
            background: #f4f5f7;
            font-size: 1rem;
        }

        .image-container {
            margin-top: 30px;
        }

        #filtered-image {
            max-width: 100%;
            height: auto;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            transition: box-shadow 0.3s;
        }

        #filtered-image:hover {
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
        }

        button {
            margin-top: 20px;
            padding: 12px 25px;
            font-size: 1rem;
            font-weight: bold;
            color: #fff;
            background-color: #4b6584;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
            transition: background-color 0.3s, transform 0.2s;
        }

        button:hover {
            background-color: #6c5ce7;
            transform: translateY(-2px);
        }

        button:active {
            transform: translateY(0);
        }
    </style>
</head>
<body>
    <div class="editor">
        <h1>Enhanced Photo Editor</h1>
        <form>
            <div>
                <label for="upload-image">Upload Image:</label>
                <input type="file" id="upload-image" accept="image/*" onchange="previewImage(event)">
            </div>
            <div class="filters">
                <div class="filter-option">
                    <label for="brightness">Brightness:</label>
                    <select id="brightness" name="brightness" onchange="applyFilters()">
                        <option value="100%">Normal (100%)</option>
                        <option value="50%">Dim (50%)</option>
                        <option value="150%">Bright (150%)</option>
                        <option value="200%">Very Bright (200%)</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="contrast">Contrast:</label>
                    <select id="contrast" name="contrast" onchange="applyFilters()">
                        <option value="100%">Normal (100%)</option>
                        <option value="50%">Low (50%)</option>
                        <option value="150%">High (150%)</option>
                        <option value="200%">Very High (200%)</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="grayscale">Grayscale:</label>
                    <select id="grayscale" name="grayscale" onchange="applyFilters()">
                        <option value="0%">Off</option>
                        <option value="100%">On</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="sepia">Sepia:</label>
                    <select id="sepia" name="sepia" onchange="applyFilters()">
                        <option value="0%">Off</option>
                        <option value="50%">Mild</option>
                        <option value="100%">Full</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="hue-rotate">Hue Rotate:</label>
                    <select id="hue-rotate" name="hue-rotate" onchange="applyFilters()">
                        <option value="0deg">None</option>
                        <option value="90deg">90 degrees</option>
                        <option value="180deg">180 degrees</option>
                        <option value="270deg">270 degrees</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="invert">Invert:</label>
                    <select id="invert" name="invert" onchange="applyFilters()">
                        <option value="0%">Off</option>
                        <option value="100%">On</option>
                    </select>
                </div>
            </div>
            <div class="image-container">
                <img id="filtered-image" src="/placeholder.svg?height=400&width=600" alt="Filtered image preview">
            </div>
        </form>
    </div>

    <script>
        <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enhanced Photo Editor</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #f3f4f7, #dcdde1);
            color: #333;
        }

        .editor {
            background-color: #fff;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        h1 {
            font-size: 2rem;
            margin-bottom: 20px;
            color: #4b6584;
        }

        .filters {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
            margin-top: 20px;
        }

        .filter-option {
            flex: 1 1 calc(33% - 20px);
            min-width: 150px;
            max-width: 200px;
            background: #f9f9f9;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .filter-option:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #57606f;
        }

        select, input[type="file"] {
            width: 100%;
            padding: 8px 10px;
            border-radius: 5px;
            border: 1px solid #dcdde1;
            background: #f4f5f7;
            font-size: 1rem;
        }

        .image-container {
            margin-top: 30px;
        }

        #filtered-image {
            max-width: 100%;
            height: auto;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            transition: box-shadow 0.3s;
        }

        #filtered-image:hover {
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
        }

        button {
            margin-top: 20px;
            padding: 12px 25px;
            font-size: 1rem;
            font-weight: bold;
            color: #fff;
            background-color: #4b6584;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
            transition: background-color 0.3s, transform 0.2s;
        }

        button:hover {
            background-color: #6c5ce7;
            transform: translateY(-2px);
        }

        button:active {
            transform: translateY(0);
        }
    </style>
</head>
<body>
    <div class="editor">
        <h1>Enhanced Photo Editor</h1>
        <form>
            <div>
                <label for="upload-image">Upload Image:</label>
                <input type="file" id="upload-image" accept="image/*" onchange="previewImage(event)">
            </div>
            <div class="filters">
                <div class="filter-option">
                    <label for="brightness">Brightness:</label>
                    <select id="brightness" name="brightness" onchange="applyFilters()">
                        <option value="100%">Normal (100%)</option>
                        <option value="50%">Dim (50%)</option>
                        <option value="150%">Bright (150%)</option>
                        <option value="200%">Very Bright (200%)</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="contrast">Contrast:</label>
                    <select id="contrast" name="contrast" onchange="applyFilters()">
                        <option value="100%">Normal (100%)</option>
                        <option value="50%">Low (50%)</option>
                        <option value="150%">High (150%)</option>
                        <option value="200%">Very High (200%)</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="grayscale">Grayscale:</label>
                    <select id="grayscale" name="grayscale" onchange="applyFilters()">
                        <option value="0%">Off</option>
                        <option value="100%">On</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="sepia">Sepia:</label>
                    <select id="sepia" name="sepia" onchange="applyFilters()">
                        <option value="0%">Off</option>
                        <option value="50%">Mild</option>
                        <option value="100%">Full</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="hue-rotate">Hue Rotate:</label>
                    <select id="hue-rotate" name="hue-rotate" onchange="applyFilters()">
                        <option value="0deg">None</option>
                        <option value="90deg">90 degrees</option>
                        <option value="180deg">180 degrees</option>
                        <option value="270deg">270 degrees</option>
                    </select>
                </div>
                <div class="filter-option">
                    <label for="invert">Invert:</label>
                    <select id="invert" name="invert" onchange="applyFilters()">
                        <option value="0%">Off</option>
                        <option value="100%">On</option>
                    </select>
                </div>
            </div>
            <div class="image-container">
                <img id="filtered-image" src="/placeholder.svg?height=400&width=600" alt="Filtered image preview">
            </div>
        </form>
    </div>

    <script>
        function previewImage(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function (e) {
                    const image = document.getElementById('filtered-image');
                    image.src = e.target.result;
                };
                reader.readAsDataURL(file);
            }
        }

        function applyFilters() {
            const brightness = document.getElementById('brightness').value;
            const contrast = document.getElementById('contrast').value;
            const grayscale = document.getElementById('grayscale').value;
            const sepia = document.getElementById('sepia').value;
            const hueRotate = document.getElementById('hue-rotate').value;
            const invert = document.getElementById('invert').value;

            const image = document.getElementById('filtered-image');
            image.style.filter = `
                brightness(${brightness}) 
                contrast(${contrast}) 
                grayscale(${grayscale}) 
                sepia(${sepia}) 
                hue-rotate(${hueRotate}) 
                invert(${invert})
            `;
        }
    </script>
</body>
</html>
    </script>
</body>
</html>
