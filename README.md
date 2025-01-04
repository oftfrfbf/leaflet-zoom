# project for creating leaflet zoom of hb0707 cruise

step 1 use test-water-column-sonar-processing 04_verify_cruise_information to generate
a png export of the Sv data. 

```
Image.fromarray(first_frequency).convert("RGB").save(f"{cruise_name}_wo_bottom.png")
```

then you will create a tile of the image. copy to out.png and then run the following steps


# If you run into memory problems just comment out all directives here.
>sudo vim /etc/ImageMagick-6/policy.xml # comment out policies

```
convert out.png -resize  x32 0.png
convert out.png -resize  x64 1.png
convert out.png -resize  x128 2.png
convert out.png -resize  x256 3.png
convert out.png -resize  x512 4.png
convert out.png -resize  x1024 5.png
convert out.png -resize  x2048 6.png
convert out.png -resize  x4096 7.png
convert out.png -resize  x8192 8.png
```
Note that size 9 uses ~60 GB of memory, so this is max usable.

```
convert -verbose 0.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/0_%[filename:tile].png"
convert -verbose 1.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/1_%[filename:tile].png"
convert -verbose 2.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/2_%[filename:tile].png"
convert -verbose 3.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/3_%[filename:tile].png"
convert -verbose 4.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/4_%[filename:tile].png"
convert -verbose 5.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/5_%[filename:tile].png"
convert -verbose 6.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/6_%[filename:tile].png"
convert -verbose 7.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/7_%[filename:tile].png"
convert -verbose 8.png -crop 512x512 +adjoin -background none -extent 512x512 -set filename:tile "%[fx:floor(page.x/512)]_%[fx:floor(page.y/512)]" +repage "tiles/8_%[filename:tile].png"
```

after this you 







