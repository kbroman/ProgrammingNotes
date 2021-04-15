## ImageMagick notes

1. replace RGB color 0,0,132 with RGB color 0,0,80

       convert meiosis_orig.png -fill 'rgb(0,0,80)' -opaque 'rgb(0,0,132)' temp.png

2. If the color is not exactly on, use "fuzz", as follows

       convert meiosis_orig.png -fill 'rgb(0,0,80)' -fuzz 10% -opaque 'rgb(0,0,132)' temp.png

3. Add white border of 5 pixels

       convert -border 5 -bordercolor white original.jpg new.jpg

4. Replace transparency with white background

       convert -flatten original.png new.png

5. convert to grayscale; make lighter

       convert input.png -colorspace Gray -gamma 2.2 output.png

6. Create thumbnail, padding to make it square
   (see <http://imagemagick.org/Usage/thumbnails/#pad>)

       wget http://www.r-project.org/Rlogo.png
       convert -flatten Rlogo.png Rlogo_new.png
       convert -define png:size=200x200 Rlogo_new.png -thumbnail \
               '64x64>' -background white -gravity center -extent 64x64 R-icon64.png

7. Pad image to a given aspect ratio (here, square to 4x6)

       convert fruitsnacks81.png -gravity center -background white -extent 150x100% fruitsnacks81_4x6.png

8. Pixelate (see <http://stackoverflow.com/questions/331254/how-to-pixelate-blur-an-image-using-imagemagick/506662#506662>)

       convert -scale 10% -scale 1000% original.jpg pixelated.jpg

9. Add white to left and white side, padding to a greater width

       convert input.png -background white -gravity northeast -splice 30x0 intermediate.png
       convert intermediate.png -background white -gravity northwest -splice 30x0 result.png

9. Resize

       convert -resize 50x100 original.png result.png

10. Resize ignoring aspect ratio

       convert -resize 50x100\! original.png result.png

11. Rotate 90 degrees clockwise

        convert -rotate "90" input.png output.png

12. Crop (width x height + left + top)

        convert -crop 587x587+0+32 original.jpg result.jpg

---

Note: [gthumb](https://wiki.gnome.org/Apps/Gthumb) is a simple GUI
image manipulator, for example for cropping.

Example swapping colors in meiosis figure

    convert meiosis.png -fill 'rgb(0,0,0)' -fuzz 5% -opaque 'rgb(255,255,255)' meiosis2.png
    convert meiosis2.png -fill 'rgb(255,255,255)' -fuzz 15% -opaque 'rgb(0,4,81)' meiosis3.png
    convert meiosis3.png -fill 'rgb(0,4,81)' -fuzz 15% -opaque 'rgb(254,102,255)' meiosis4.png

---

no support for HEIC files yet, so do (see [here](https://askubuntu.com/a/1108325)):

    sudo apt install libheif-examples
    heif-convert myfile.heif myfile.jpg
