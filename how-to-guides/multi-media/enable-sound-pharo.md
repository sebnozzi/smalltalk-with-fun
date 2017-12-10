# Enable sound support in Pharo

Unlike Squeak, Pharo does not come with sound-support enabled by default. For that you need to import the packages "PharoSound".

Open the "Catalog Browser" by clicking on an empty area of the Pharo desktop, and then selecting it from the "Tools" menu like this:

![](/assets/open-catalog-browser.png)

Once in the "Catalog Browser", filter the packages by writing "sound" or "pharosound".

![](/assets/filter-pharosound.png)

You should see the "PharoSound" package. Install the stable version by doing either of these:

* Click on the green checkmark in the "Catalog Browser" toolbar
* Alternatively, right-Click on the "PharoSound" package and select "Install stable version".

![](/assets/install-pharosound.png)

Test it with this code:

```smalltalk
SampledSound beep.
```

You should hear the sound of "the sound of a spoon being tapped against a coffee cup" \(with an echo\).

