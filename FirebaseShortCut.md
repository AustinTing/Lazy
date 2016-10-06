FirebaseShortCut
=====
基本
----
三個版本號必須相同:
```gradle
compile 'com.google.firebase:firebase-auth:9.6.1'
compile 'com.google.firebase:firebase-database:9.6.1'
compile 'com.google.android.gms:play-services-auth:9.6.1'
```

宣告:
```java
FirebaseAuth auth;
DatabaseReference dbRef;
auth = FirebaseAuth.getInstance();
dbRef = FirebaseDatabase.getInstance().getReference();
```
記得rule注意  
新增使用者:
```java
String name = auth.getCurrentUser().getDisplayName();
String imgUrl = auth.getCurrentUser().getPhotoUrl().toString();
User user = new User(name, imgUrl);
String uid = auth.getCurrentUser().getUid();
dbRef.child("users").child(uid).setValue(user);
```
上傳資料:
```java
Post post = new Post(userUrl,System.currentTimeMillis(), sub, dsc, 0, 0);
String key = dbRef.child("posts").push().getKey();
String uid = auth.getCurrentUser().getUid();
dbRef.child("post").child(key).setValue(post);
dbRef.child("user-post").child(uid).child(key).setValue(post);
```
一次性下載資料:
```java
dbRef.child("image").limitToLast(1).addListenerForSingleValueEvent(new ValueEventListener() {
    @Override
    public void onDataChange(DataSnapshot dataSnapshot) {
      for (DataSnapshot data : dataSnapshot.getChildren()) {
        Log.d(TAG, "PostActivity: data: "+data.getValue());
        Image image = data.getValue(Image.class);
       }
    }
    @Override
    public void onCancelled(DatabaseError databaseError) {
      Log.e(TAG, "PostActivity: onCancelled: " + databaseError.getDetails());
    }
});
```
FirebaseRecyclerAdapter
------
宣告:
```java
RecyclerView recyclerView;
LinearLayoutManager linearLayoutManager;

```
onCreate:
```java
linearLayoutManager = new LinearLayoutManager(this);
// 讓列表資料反轉 THIS ALSO SETS setStackFromBottom to true
linearLayoutManager.setReverseLayout(true);
linearLayoutManager.setStackFromEnd(true);
recyclerView.setHasFixedSize(true);
recyclerView.setLayoutManager(linearLayoutManager);
```

內部類別:
```java
public static class ItemViewHolder extends RecyclerView.ViewHolder {

        public final static int layoutResId = R.layout.ac_main_item;
        CircleImageView userImage;

        public ItemViewHolder(View view) {
            super(view);
            userImage = (CircleImageView) view.findViewById(R.id.userImage);
        }
    }
```
onStart:
```java
FirebaseRecyclerAdapter<Event, ItemViewHolder> adapter =
                new FirebaseRecyclerAdapter<Event, ItemViewHolder>(
                        Event.class,
                        ItemViewHolder.layoutResId,
                        ItemViewHolder.class,
                        dbRef.child("post")
                        ) {
            @Override
            protected void populateViewHolder(ItemViewHolder viewHolder, Event event, int position) {
                ImageLoader.getInstance().displayImage(event.getUserImgUrl(), viewHolder.userImage);
                //  取得這個item的key
                getRef(i).getKey()
            }
        };
recyclerView.setAdapter(adapter);
```


