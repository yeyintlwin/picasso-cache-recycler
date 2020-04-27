# Android Picasso-Library Cache Recycler

Get bitmap from [picasso](http://github.com/square/picasso) cache.
Usage: `getBitmap(context, url)`


```java
public static Bitmap getBitmap(Context context, String url) {
        final String CACHE_PATH = context.getCacheDir().getAbsolutePath() + "/picasso-cache/";
        File[] files = new File(CACHE_PATH).listFiles();
        for (File file : files) {
            String fname = file.getName();
            if (fname.contains(".") && fname.substring(fname.lastIndexOf(".")).equals(".0")) {
                try {
                    BufferedReader br = new BufferedReader(new FileReader(file));
                    if (br.readLine().equals(url)) {
                        String image_path = CACHE_PATH + fname.replace(".0", ".1");
                        if (new File(image_path).exists()) {
                            return BitmapFactory.decodeFile(image_path);
                        }
                    }
                } catch (FileNotFoundException | IOException e) {
                }
            }
        }
        return null;
    }
```
