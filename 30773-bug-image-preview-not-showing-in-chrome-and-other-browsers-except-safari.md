# Bug: Image Preview Not Showing in Chrome and Other Browsers Except Safari

> Issue #30773 - Created on 8/21/2024

> Original URL: https://github.com/facebook/react/issues/30773

## Description

## **Description:**

The image preview functionality in my React application is not working as expected in Chrome and other browsers (like Firefox or Edge), while it works fine in Safari. The issue occurs when trying to preview an image file uploaded through an input field.

**React version:** 18.3.1

## Code Snippets
```js
const handleImageChange = (e) => {
    const file = e.target.files[0];

    if (file) {
      const previewURL = URL.createObjectURL(file);
      setImagePreview(previewURL);
      setValue("profileImage", file);
    }
  };
```
```js
<form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label htmlFor="profileImage">Profile Image:</label>
        <input
          type="file"
          name="profileImage"
          accept="image/*"
          ref={fileInputRef}
          onChange={handleImageChange}
          {...register('profileImage', { required: "Profile image is required" })}
        />
        {errors.profileImage && <ErrorMessage>{errors.profileImage.message}</ErrorMessage>}
      </div>
      
      {imagePreview && <FilePreview file={imagePreview} />}
      
      <button type="submit">Register</button>
</form>
```

## The current behavior

- The image preview is not displayed in Chrome and other browsers.
- No errors are visible in the browser's console.
- The preview functionality works as expected in Safari.

## The expected behavior

- The image preview should be displayed in all modern browsers, including Chrome, Firefox, and Edge, in addition to Safari.
- The preview should update whenever a new image file is selected.

