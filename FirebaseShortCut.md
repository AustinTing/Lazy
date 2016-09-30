FirebaseShortCut
=====
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
        
