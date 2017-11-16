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

9. Resize

       convert -resize 50x100 original.png result.png

10. Resize ignoring aspect ratio

       convert -resize 50x100\! original.png result.png
