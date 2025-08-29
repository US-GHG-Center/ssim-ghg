# Checkout instructions
## For people with write/commit access
### Configure git so that output cells of ipython notebooks are stripped before committing
* Install `jupyter` (platform-dependent)
* Install `nbconvert` (platform-dependent)
* Ensure that `jupyter nbconvert` on the command line on your system gives _some_ output. Typically it will print a help or usage message. If it says `Jupyter command jupyter-nbconvert not found` then there is a problem, i.e., the following steps will not work on your system.
* Modify `~/.gitconfig` with the following section
  ```
  [filter "strip-notebook-output"]
      clean = "jupyter nbconvert --ClearOutputPreprocessor.enabled=True --ClearMetadataPreprocessor.enabled=True --to=notebook --stdin --stdout --log-level=ERROR"
  ```
  Alternatively, you can add the above block to your `.git/config` _after_ you checkout the repo but _before_ you do any other git operation, even seemingly read-only operations such as `git status`. If you do this, then the "strip notebooks of output and metadata" filter will only apply to this repo and not globally to all your git repos. Your choice.

### Check out code
```
git clone git@github.com:US-GHG-Center/ssim-ghg.git ssim-ghg
```
This will check out the code in a folder called `ssim-ghg`. Alternatively, you can change the target name to something else by changing that last element in the command above. E.g., to check out the code to `math-camp-examples` execute
```
git clone git@github.com:US-GHG-Center/ssim-ghg.git math-camp-examples
```

### Verify that committing strips the output
Make sure that you have the `strip-notebook-output` filter as described above either in your global `~/.gitconfig` or the repository's `.git/config`. Open any of your own notebooks, change the output, then try to commit/push with `git add`, `git commit` and `git push`.

## For people with read-only access

Check out the code with
```
git clone https://github.com/US-GHG-Center/ssim-ghg.git ssim-ghg
```

# Downloading input data

Download input data from our [zenodo archive](https://doi.org/10.5281/zenodo.14291546) and decompress it somewhere.

# Configuring paths
Copy over `site_settings.yml.tmpl` to `site_settings.yml` and modify accordingly. Specifying a font for the plots is optional, but you at least need to specify an input and an output folder, and the location of `absco.h5` if you want to run the retrieval example. __Do not add `site_settings.yml` to the git repository__. Since this file contains platform-specific paths, it makes no sense to have different people try to push conflicting versions of this file.
