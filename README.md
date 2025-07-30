<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CKEditor 5 Example</title>
  <script src="https://cdn.ckeditor.com/ckeditor5/41.0.0/classic/ckeditor.js"></script>
  <style>
    .editor-container {
      width: 80%;
      margin: 50px auto;
    }
  </style>
</head>
<body>

  <div class="editor-container">
    <h2>CKEditor 5 Demo</h2>
    <textarea name="content" id="editor"></textarea>
  </div>

  <script>
    ClassicEditor
      .create(document.querySelector('#editor'))
      .catch(error => {
          console.error(error);
      });
  </script>

</body>
</html>
