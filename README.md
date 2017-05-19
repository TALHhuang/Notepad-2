# NotePad
This is an AndroidStudio rebuild of google SDK sample NotePad


一 功能扩展<br>
   1.显示条目增加时间戳显示<br>
   2.添加笔记查询功能<br>
   3.UI美化<br>
   4.更改记事本的背景<br>
   
   
二 功能展示<br>
   1.TALH Notepad 登入进去的主界面<br><br>
   ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/1.png)
   <br><br>
   2.按笔记的标题查询笔记(在搜索框中输入要查询的笔记的TITLE然后点击右边的搜索按钮.以下是查询One为TITLE的笔记内容）<br><br>  
      ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/2.png)
      <br><br>
      
          public void Search(String searchTitle){
                 searchData=new ArrayList<NoteBean>();
                  for(NoteBean noteBean:mDate){
                       if(noteBean.getTitle().equals(searchTitle)){
                              searchData.add(noteBean);
                     }
                   }
                   mDate.clear();
                   mDate.addAll(searchData);
                    notifyDataSetChanged();
              }
   3.新建一个笔记（点击屏幕右下方的粉红色加号按钮进入新建界面新建笔记，输入完后点击屏幕上方的保存按钮保存）<br><br>
      ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/3.png)
      <br><br>
     （新建一个TALH标题后的主界面）<br><br>
      ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/4.png)
      <br><br>
    4.删除笔记（点击每一条笔记右边的小笔按钮进入编辑界面。然后点击屏幕上方的删除按钮删除笔记）<br><br>
      ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/6.png)
      <br><br>
      （删除以TALH为标题笔记后的主界面）<br><br>
      ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/7.png)   
      <br><br>
    5.编辑笔记（点击小笔图案进入编辑界面进行笔记编辑。编辑后主界面显示该笔记最新的编辑时间）<br><br>
       （以编辑 Six two five 为例）<br><br>
       ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/8.png)  
       ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/7.png)  
       ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/9.png)
       
       (自己定义一个适配器，详情见工程里面的代码）
       
            public void readDate()
             {
                 mDate.clear();
                  while(cursor.moveToNext())
                  {
                      mDate.add(new NoteBean(cursor.getString(COLUMN_INDEX_TITLE),
                      cursor.getString(COLUMN_INDEX_MODIFICATION_DATE),
                      cursor.getString(COLUMN_INDEX_ID)));
                      Log.d("hhh",cursor.getString(COLUMN_INDEX_TITLE)+
                      ","+cursor.getString(COLUMN_INDEX_MODIFICATION_DATE)+
                      ","+cursor.getString(COLUMN_INDEX_ID));
                   }
             }
       <br><br><br><br><br>
 三 UI美化<br>
    1.item进行美化，然后添加了 `Floating Action Button` (Android floating action button which reacts on scrolling events. Becomes visible when an attached target is scrolled up and invisible when scrolled down.上划按钮消失，下滑按钮出现）<br><br>
     （`Floating Action Button`效果的百度图片    `注意看右下方的按钮`）<br><br>
    ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/FloatingActionButton.gif)
    <br><br>
      (我的 TALH Notepad 程序中该功能的截图，有兴趣的可以下载我的程序去玩玩，效果跟上面效果图一样)
     ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/5.png)  
     ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/4.png)  
     <br><br>
     
             FloatingActionButton fab = (FloatingActionButton) findViewById(R.id.fab);
             fab.attachToListView(lv_notesList);
             fab.setBackgroundResource(R.drawable.ic_launcher);
             
             
         <FrameLayout
          android:layout_width="match_parent"
          android:layout_weight="1"
          android:orientation="vertical"
         android:layout_height="match_parent">
         <ListView
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           android:cacheColorHint="#00000000"
           android:divider="#FFFFCC"
           android:dividerHeight="0dp"
           android:id="@id/android:list">
         </ListView>
            <com.melnykov.fab.FloatingActionButton
            android:id="@+id/fab"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_gravity="bottom|right"
            android:layout_margin="16dp"
            />
        
     2.更改背景颜色（点击主屏幕右上角的菜单按钮，然后点击 Change Color 选项。再选择自己喜欢的颜色进行更改）<br><br>
      ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/11.png) 
      ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/12.png)  
      ![photo](https://github.com/TALHhuang/Notepad-2/blob/master/photo/13.png)  
     <br><br>
     
          private  void showpopSelectBgWindows(){
          LayoutInflater inflater = LayoutInflater.from(this);
          View view = inflater.inflate(R.layout.dialog_bg_select_layout, null);
          AlertDialog.Builder builder = new AlertDialog.Builder(this);
          builder.setTitle("背景");
          builder.setView(view);
          AlertDialog dialog = builder.create();
          dialog.show();
          }


                      color="#7FFF00";
                      ll_noteList.setBackgroundColor(Color.parseColor(color));
                      lv_notesList.setBackgroundColor(Color.parseColor(color));
                      adapter.setBackground(color);
                      adapter.notifyDataSetChanged();
                      MyApplication.setBackground(color);
                      MyApplication.saveBackground();
                    
   <br><br><br><br><br>
   `全部的功能如何实现请看代码`
            
