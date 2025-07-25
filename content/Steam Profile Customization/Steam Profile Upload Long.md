
This guide explains how to upload Steam artworks or screenshots as long images by using browser developer console commands.

---

## Steps

1. **Open Steam Artwork Upload Page**  
   Open the following URL in **Google Chrome** or **Mozilla Firefox**:  
   [https://steamcommunity.com/sharedfiles/edititem/767/3/](https://steamcommunity.com/sharedfiles/edititem/767/3/)

2. **Select Your Artwork**  
   Click **Choose File** and select the image or GIF you want to upload.

3. **Open Browser Console**  
   - **Google Chrome:** Press `Ctrl + Shift + J`  
   - **Mozilla Firefox:** Press `Ctrl + Shift + K`  
   Alternatively, right-click anywhere on the page, select **Inspect** or **Inspect Element**, then go to the **Console** tab.

4. **Paste the Appropriate Code in the Console**  
   Use **only one** of the following code snippets depending on the upload type.

   - **For Artwork or Featured Artwork:**

```javascript
$J('#image_width').val(1000).attr('id',''),$J('#image_height').val(1).attr('id','');
```

* For Screenshot:

```javascript
$J('#image_width').val(1000).attr('id',''),$J('#image_height').val(1).attr('id',''),$J('[name=file_type]').val(5);
```
5. **Ignore Image Preview**  
The preview may not display correctly, but the last selected image or GIF will be uploaded.
6. **Complete the Upload**

	- Enter a title for your artwork.
	    
	- Tick the checkbox: _"I certify that I created this artwork"_.
	    
	- Click **Save and Continue**.
## Notes

- This method forces Steam to treat the artwork as a **long image** (width 1000px and height 1px) for vertical display.
    
- Use the appropriate snippet for artwork type to ensure correct classification.
    
- This process requires basic familiarity with browser developer tools.