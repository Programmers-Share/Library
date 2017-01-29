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
                  DocumentFile pickedDir = DocumentFile.fromTreeUri(this, sdCardUri);
                  grantUriPermission(getPackageName(), sdCardUri, Intent.FLAG_GRANT_READ_URI_PERMISSION | Intent.FLAG_GRANT_WRITE_URI_PERMISSION);
                  getContentResolver().takePersistableUriPermission(sdCardUri, Intent.FLAG_GRANT_READ_URI_PERMISSION | Intent.FLAG_GRANT_WRITE_URI_PERMISSION);
              }
              break;
      }
  }
</PRE>
