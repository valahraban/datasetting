# Datasetting
This repository was originally meant for publishing original text datasets for NLP uses. I have since reconsidered and abandoned this goal. But since this repository received Stars, I'm keeping it up for historic reasons and continuing to provide a collection of tools that may help in collecting and formatting your own text datasets. Documents under this repository are licensed under the GFDL. Most fandoms operate under CC BY-SA 3.0 so citation for both licenses is provided.  

## License Declaration
https://www.gnu.org/licenses/fdl-1.3.html  
https://creativecommons.org/licenses/by-sa/3.0/

## How to collect and extract textual data
Obtain a dump of the wiki you wish to extract data from. For fandom this can be done by visiting the **Special:Statistics** category and finding the bolded link for **Current pages**. Then you should download and star the script I use and link below:  
```
https://github.com/josecannete/wikiextractorforBERT
```
I recommend running the WikiExtractor fork with the following example arguments (which you have to modify for your folders):  
```
python WikiExtractor.py ~/Datasetting/samplefandomdump_pages_current.xml -o ~/Datasetting/extractedfolder --for-bert --filter_category "my_categories.txt"
```
`my_categories.txt` is a file you have to make yourself to support the `--filter_category` argument. Every newline starts with the name of a category (you don't use the *Category:* namespace for this). If a line starts with the letter `#` it will be commented out. If a line starts with `^` the category following it will be exluded from the extraction, this is useful for filtering sub-categories. By reading the source of WikiExtractor.py you can find all of its arguments, but I find `--for-bert` and filtering by category takes care of most of the work for datasetting.

josecannete's fork was intended for use with BERT, but I believe the outputted txt files work good enough for use with any model. You will still have to do thorough vetting and curation on the result files with your favorite text editor tools to ensure the quality is good enough for whatever finetune application you have in mind.  

After you're done modifying the files and are satisfied with your formatting you may want to merge them if there are multiple. This can be done on a terminal with:  
```
cat extractedfolder/*/* > fandom.txt
```
If for some reason you get weird and unsatisfactory output you can't fix with WEB this is due to automatic templates being broken in modern versions of WE. If you need template functionality, you need an older version of WE. You can grab it [here](https://web.archive.org/web/20201120105747/http://medialab.di.unipi.it/Project/SemaWiki/Tools/WikiExtractor.py). This version requires Python 2.7.18!

It works with the same commands and arguments as regular WE. The resulting text files need extra cleaning which can be accomplished with Python scripts I've linked in my repositories.
