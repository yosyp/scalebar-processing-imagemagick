# Last modified <2017-06-20 Tue> by @yosyp 
# Focus stacking and aligning images
## Align
```
align_image_stack -v -m -a OUT *
```

## Focus Stack
```
enfuse --exposure-weight=0 --saturation-weight=0 --contrast-weight=1 --hard-mask --output=final.tif OUT*.tif
enfuse --exposure-weight=0 --saturation-weight=0 --contrast-weight=1 --hard-mask --output=50x-focused.tif 50x-fs*.TIF
```

# Scalebars image editing
## Delete matches
```
for d in ./*/; do (
    cd "$d/with-scalebars" &&
    rm 04x*.tif
    ); done
	```
	
## Scalebars in batch
```
for d in ./*/; do (
    cd "$d" && 
    mkdir with-scalebars &&
    for f in 04x*.TIF; do (
        convert -gravity southeast "$f" ~/disk2/ctp\ samples/Microscope\ Objective\ References/04x-500um.tif -geometry +40+30 -composite with-scalebars/"${f%.*}"-scalebar.tif &&
        echo "finished $d/$f");
    done &&
    for f in 10x*.TIF; do (
        convert -gravity southeast "$f" ~/disk2/ctp\ samples/Microscope\ Objective\ References/10x-250um.tif -geometry +40+30 -composite with-scalebars/"${f%.*}"-scalebar.tif &&
        echo "finished $d/$f");
    done &&
    for f in 20x*.TIF; do (
        convert -gravity southeast "$f" ~/disk2/ctp\ samples/Microscope\ Objective\ References/20x-100um.tif -geometry +40+30 -composite with-scalebars/"${f%.*}"-scalebar.tif &&
        echo "finished $d/$f");
    done &&
    for f in 50x*.TIF; do (
        convert -gravity southeast "$f" ~/disk2/ctp\ samples/Microscope\ Objective\ References/50x-100um.tif -geometry +40+30 -composite with-scalebars/"${f%.*}"-scalebar.tif &&
        echo "finished $d$f");
    done );
done
```

## Add scalebars to focus stacked images too
```
	for f in 50x-foc*.tif; do (
        convert -gravity southeast "$f" /media/asdf/disk2/ctp\ samples/Microscope\ Objective\ References/50x-100um.tif -geometry +40+30 -composite with-scalebars/"${f%.*}"-scalebar.tif &&
        echo "finished $d$f");
    done &&
    for f in 20x-foc*.tif; do (
        convert -gravity southeast "$f" /media/asdf/disk2/ctp\ samples/Microscope\ Objective\ References/20x-100um.tif -geometry +40+30 -composite with-scalebars/"${f%.*}"-scalebar.tif &&
        echo "finished $d/$f");
    done &&
    for f in 10x-foc*.tif; do (
        convert -gravity southeast "$f" /media/asdf/disk2/ctp\ samples/Microscope\ Objective\ References/10x-0um.tif -geometry +40+30 -composite with-scalebars/"${f%.*}"-scalebar.tif &&
        echo "finished $d/$f");
    done
```
