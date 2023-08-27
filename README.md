# Wildcards
This extension version is meant to work in pair with this version of [after-detailer](https://github.com/Cryptik-Rick/sd-webui-adetailer) by keeping track of what wildcard has been replaced with, and applying the same wildcard to after detailer's inpainting.

It will work with the base version, but by replacing any wildcard with a random one. This is the first version, and I intend to improve it with a couple quality of life options. See [Upcomming features](#upcomming_features) for more details.

## Features
 * Use `__name__` syntax in your prompt to get a random line from a file named `name.txt` in the wildcards directory.
 * Use `[__name__]` in the adetailer prompt to get fill in the prompt with the same name that was generated.
 * Or use `__name__` in the adetailer's prompt to generate a new random one.
 * zip file with the wildcards I use included. Just unzip to use.

## Install
**Very important:** A line of code needs to be added to the base after-detailer extension in order to keep track of which image we are processing. You can [add the line yourself](#adding_the_line_yourself), or follow the instructions below:

1. If stable-diffusion-webui-wildcards is already installed, make a copy of your wildcards folder, as these will get deleted.
1. Make sure the the following extensions are **uninstalled**: stable-diffusion-webui-wildcards, adetailer, sd-dynamic-prompts See [uninstalling extensions](#uninstalling_extensions) for more details
1. Open "Extensions" tab.
1. Open "Install from URL" tab in the tab.
1. Enter https://github.com/Cryptik-Rick/sd-webui-wildcards-ad.git to "URL for extension's git repository".
1. Press "Install" button.
1. Wait 5 seconds, and you will see the message "Installed into stable-diffusion-webui\extensions\sd-webui-wildcards-ad."
1. Enter https://github.com/Cryptik-Rick/sd-webui-adetailer.git to "URL for extension's git repository".
1. Press "Install" button.
1. Wait 5 seconds again and you will see the message "Installed into stable-diffusion-webui\extensions\sd-webui-adetailer."
1. Go to "Installed" tab, click "Check for updates", and then click "Apply and restart UI". (The next time you can also use this method to update extensions.)
1. Replace the wildcards folder with the backup you made (if applicable)
1. Completely restart A1111 webui including your terminal (black screen that appears when you start automatic 1111).

### Uninstalling extensions
If you do not know how to uninstall extension, here's a rundown:

1. Stop A1111 webui by closing your terminal (black screen that appears when you start automatic 1111).
1. Navigate to your A1111's install location and then into extensions
1. Manually delete the extension's folders

## Install manually
Alternatively, to install by hand:

1. Make sure the the following extensions are **uninstalled**: stable-diffusion-webui-wildcards, adetailer, sd-dynamic-prompts See [uninstalling extensions](#uninstalling_extensions) for more details
2. From your base `stable-diffusion-webui` directory, run the following commands to install:
    ```
    git clone https://github.com/Cryptik-Rick/sd-webui-wildcards-ad.git extensions/sd-webui-wildcards-ad
    git clone https://github.com/Cryptik-Rick/sd-webui-adetailer.git extensions/sd-webui-adetailer
    ```

Then restart the webui.

## Adding the line yourself

On line 424, right below the `i2i = StableDiffusionProcessingImg2Img` class instanciation, add the line `i2i._ad_idx = p._ad_idx`:

```python{7}
            extra_generation_params=p.extra_generation_params,
            do_not_save_samples=True,
            do_not_save_grid=True,
            override_settings=override_settings,
        )

        i2i._ad_idx = p._ad_idx
        i2i.cached_c = [None, None]
        i2i.cached_uc = [None, None]
        i2i.scripts, i2i.script_args = self.script_filter(p, args)
```

## Upcomming features
 - [ ] Making a settings menu.
 - [ ] "Replace wildcards" option instead of the inline brackets.
 - [ ] adetailer's PNG info with wildcards replaced (the main one is fine, adetailer's one will still show the one before wildcards).
 - [ ] Support of wildcards in negative prompts (which the base wildcard extension doesn't support right now).
 - [ ] Many improvements on adetailer and wildcards.
