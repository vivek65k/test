<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CKEditor 4 Example</title>
  <script src="https://cdn.ckeditor.com/4.21.0/standard/ckeditor.js"></script>
  <style>
    .editor-container {
      width: 80%;
      margin: 50px auto;
    }
  </style>
</head>
<body>

  <div class="editor-container">
    <h2>CKEditor 4 Demo</h2>
    <textarea name="content" id="editor"></textarea>
  </div>

  <script>
    CKEDITOR.replace('editor');
  </script>

</body>
</html>
