# Indexing Image Stacks

Volume processing often requires indexing the stack to pull out smaller stacks or individual slices.

Indexing image stacks is fairly straightforward — you just need to keep track of the Dimensions. For example, if we have a 4D volume, `RGB4`, with dimensions `512x512x3x12`, we can index out the Red channel using the following syntax:

```matlab linenums="1" title="Index out the Red Channel"
RED = RGB4(:,:,1,:); % all rows, all columns, channel 1, all z-slices
```

…This returns a 4D array with just 1 channel

```matlab title="Size of RED"
size(RED)

ans =

   512   512     1    12
```

We can drop the singleton dimension (dimension three) using the function **squeeze**.

```matlab title="Squeeze 4D array into a 3D array"
RED = squeeze(RED);

size(RED)

ans =

   512   512   12
```

…Now *`RED`* is a 3D array.

We can index a single slice out of *`RED`* using the following syntax:

```matlab linenums="1" title="Indexing out the Sixth Slice from RED"
slice = RED(:,:,6)
```

```matlab title="Size of slice"
size(slice)

ans =

   512   512
```

…*`slice`* is a `512x512` image.

If we wanted all three channels in a slice, we simply index the original, 4D volume, *`RGB4`*.

```matlab linenums="1" title="Index out 6th Slice from RGB4"
rgb_slice = RGB4(:,:,:,6); % all rows, all columns, all channels, slice 6
```

```matlab title="Size of slice"
size(rgb_slice)

ans =

   512   512   3
```

…*`rgb_slice`* is an image with 3 channels (RGB image).

So, we can index out a color channel by accessing the third dimension and index out a z-plane by accessing the 4th dimension.