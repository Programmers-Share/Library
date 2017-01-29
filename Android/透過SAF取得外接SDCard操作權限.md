#前言

在Android中，SDCard有分成兩種

1. 手機內附SDCard
2. 外接SDCard

如果是第一種，只需要在`AndroidManifest.xml`中加入以下權限即可操作

<PRE>
  &lt;uses-permission android:name=&quot;android.permission.WRITE_EXTERNAL_STORAGE&quot; /&gt;
  &lt;uses-permission android:name=&quot;android.permission.READ_EXTERNAL_STORAGE&quot; /&gt;
</PRE>

對於第二種，4.4(KitKat)版之後因GOOGLE政策關係，已經拒絕第三方APP在data資料夾外做操作，原因眾說紛紜

但在5.0(Lollipop)版後，大概是因為很多開發者的抱怨(?)，GOOGLE擴充了[SAF(Storage Access Framework)](https://developer.android.com/guide/topics/providers/document-provider.html)的功能

使得開發者又可以對SDCard為所欲為了(?)

#Step 1

<PRE>
  static final int DIRECTORY_CHOOSE_REQ_CODE = 42;
  
  private void performDirectoryChoose(){
    Intent intent  = new Intent(Intent.ACTION_OPEN_DOCUMENT_TREE);
    startActivityForResult(intent, DIRECTORY_CHOOSE_REQ_CODE);
  }
  
  @Override
  protected void onActivityResult(int requestCode, int resultCode, Intent data) {
      super.onActivityResult(requestCode, resultCode, data);
      switch (requestCode){
          case DIRECTORY_CHOOSE_REQ_CODE:
              if (resultCode == Activity.RESULT_OK) {
                  Uri sdCardUri = data.getData();
                  grantUriPermission(getPackageName(), sdCardUri, Intent.FLAG_GRANT_READ_URI_PERMISSION | Intent.FLAG_GRANT_WRITE_URI_PERMISSION);
                  getContentResolver().takePersistableUriPermission(sdCardUri, Intent.FLAG_GRANT_READ_URI_PERMISSION | Intent.FLAG_GRANT_WRITE_URI_PERMISSION);
              }
              break;
      }
  }
</PRE>

呼叫`performDirectoryChoose`後，按照下列步驟選擇

![01](https://github.com/Programmers-Share/Library/blob/master/Android/img/SAF-SDCard/01.png)

![02](https://github.com/Programmers-Share/Library/blob/master/Android/img/SAF-SDCard/02.png)

![03](https://github.com/Programmers-Share/Library/blob/master/Android/img/SAF-SDCard/03.png)

![04](https://github.com/Programmers-Share/Library/blob/master/Android/img/SAF-SDCard/04.png)

選擇完畢之後系統會去呼叫覆寫的`onActivityResult`方法

> Uri sdCardUri = data.getData();
  
這一行是取到剛剛使用者所選擇的Uri

**非絕對位置 Ex. /tree/3461-3532**

> grantUriPermission(getPackageName(), sdCardUri, Intent.FLAG_GRANT_READ_URI_PERMISSION | Intent.FLAG_GRANT_WRITE_URI_PERMISSION)

這一行是要求上面Uri的權限，這邊是要求讀跟寫

> getContentResolver().takePersistableUriPermission(sdCardUri, Intent.FLAG_GRANT_READ_URI_PERMISSION | Intent.FLAG_GRANT_WRITE_URI_PERMISSION);

這一行是讓權限永久化，如此一來就算手機重開機後也不會遺失權限

**但換了一張SDCard還是得要從來一遍**

#Step 2

<PRE>
  private DocumentFile df;
  private boolean checkHasSDCard1PermissionAndSetParam(){
      DocumentFile df;
      for (UriPermission p: getContentResolver().getPersistedUriPermissions()) {
          df = DocumentFile.fromTreeUri(this, p.getUri());
          if (df.canRead() && "sdcard1".equals(df.getName())){
              this.df = df;
              return true;
          }
      }

      return false;
  }
</PRE>

[DocumentFile](https://developer.android.com/reference/android/support/v4/provider/DocumentFile.html)是一個把File類別再包裝的類別，詳細介紹可以參考官方文件

> getContentResolver().getPersistedUriPermissions()

這一行是取出已有的權限，回傳一個`UriPermission`陣列

> "sdcard1".equals(df.getName())

**sdcard1**是外接SDCard的固定名稱，所以如果有配對到表示有要求到權限

#結論

雖然對於GOOGLE為什麼對外接SDCard做了限制而感到不解

但好險在5.0版本後有推出另類的解決方案，不然檔案管理的APP就GG了

花了一天試驗加找資料，寫篇文章記錄一下，希望可以幫到遇到相同問題的開發者們
