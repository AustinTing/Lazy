##9 patch
####使用
  1. 圖片放到drawable下面
  1. 右鍵create 9patch，新檔依舊放在drawable下面，刪除原來那張
  1. 編輯9patch
  
####設成背景
  - layout要有`padding`屬性，要不然會蓋住其他層   
  >  [Android Api](https://developer.android.com/guide/topics/graphics/2d-graphics.html#nine-patch) "You can also define an optional drawable section of the image (effectively, the padding lines) by drawing a line on the right and bottom lines. If a View object sets the NinePatch as its background and then specifies the View's text, it will stretch itself so that all the text fits inside only the area designated by the right and bottom lines (if included). **If the padding lines are not included, Android uses the left and top lines to define this drawable area.**"
  
####在layer-list裡面
  - 要下透明度，記得要設定`dither`
  
  ```
  <item>
    <nine-patch
      android:src="@drawable/floral"
      android:alpha="0.1" 
      android:dither="true"
      />
  </item>
  ```
  
  
   
