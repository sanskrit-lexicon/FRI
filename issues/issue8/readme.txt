# Frish issue8
Latin to Cyrillic
ref: https://github.com/sanskrit-lexicon/FRI/issues/8

cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home

* temp_fri_0.txt
# Get current fri.txt from csl-orig
cd /c/xampp/htdocs/cologne/csl-orig
git log | head -n 1  # get latest commit hash
# commit 7140e09c08f3addf4a3867ba09759c1d636faf46
-- local copy of fri in issue8
git show 7140e09c:v02/fri/fri.txt > /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8/temp_fri_0.txt
cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home

python unixify.py temp_fri_1.txt temp_fri_1a.txt

----------------------------
* temp_fri_1.txt (the revised file)
# downloaded as /Downloads/fri.txt from
#  https://github.com/sanskrit-lexicon/FRI/issues/8#issuecomment-3996839445
cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home
cp ~/Downloads/fri.txt temp_fri_1.txt

# compare number of lines in the two versions:
wc -l temp_fri*.txt
  47478 temp_fri_0.txt
  47478 temp_fri_1.txt
# same number of lines

# preliminary comparison
diff temp_fri_0.txt temp_fri_1.txt | wc -l
# 94958
# completely different! Not expected.
# probably a 'line-ending' difference.
# cdsl standard line-end in csl-orig files is unix '\n'

Use a python program to change to '\n'
python unixify.py temp_fri_1.txt temp_fri_1a.txt
# 47478 lines written to temp_fri_1a.txt

# try the diff with 1a
diff temp_fri_0.txt temp_fri_1a.txt | wc -l
# 3360 -- that's more like it!

(/ 3360 4) 840  approximately 840 lines changed.

* diff_fri_0_1a.txt
diff temp_fri_0.txt temp_fri_1a.txt > diff_fri_0_1a.txt

-------------------------------------------------
* change_fri_0_1a.txt  another way to see the changes
python diff_to_changes_dict.py temp_fri_0.txt temp_fri_1a.txt change_fri_0_1a.txt

# 849 changes written to change_fri_0_1a.txt

-------------------------------------------------
# regenerate local display using temp_fri_1a.txt
cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home
cp temp_fri_1a.txt /c/xampp/htdocs/cologne/csl-orig/v02/fri/fri.txt
cd /c/xampp/htdocs/cologne/csl-pywork/v02
sh generate_dict.sh fri  ../../fri

----------------------------------------------------------
# WARNING: make_xml.py: 2 records records not parsed by ET
# Resolve by editing with emacs (to check validity of fri.xml)
 /c/xampp/htdocs/cologne/fri/pywork/fri.xml
cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home
cp temp_fri_1a.txt temp_fri_2.txt
# make corrections in temp_fri_2.txt

-------------------------------------------------
# regenerate local display using temp_fri_2.txt
cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home
cp temp_fri_2.txt /c/xampp/htdocs/cologne/csl-orig/v02/fri/fri.txt
cd /c/xampp/htdocs/cologne/csl-pywork/v02
sh generate_dict.sh fri  ../../fri
# Warning message gone.
# Further check that fri.xml is valid
sh xmlchk_xampp.sh fri
python3 ../../xmlvalidate.py ../../fri/pywork/fri.xml ../../fri/pywork/fri.dtd
# ok   (fri.xml is valid)

-------------------------
document the changes of version 2
cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home
python diff_to_changes_dict.py temp_fri_1a.txt temp_fri_2.txt change_fri_1a_2.txt
2 changes written to change_fri_1a_2.txt

----------------------------
# install temp_fri_2.txt change to github, etc.
cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home
cp temp_fri_2.txt /c/xampp/htdocs/cologne/csl-orig/v02/fri/fri.txt

cd /c/xampp/htdocs/cologne/csl-orig
git add .
git status
# modified:   v02/fri/fri.txt
git commit -m "fri: Latin to Cyrillic strings.
Ref: https://github.com/sanskrit-lexicon/FRI/issues/8"
# 1 file changed, 847 insertions(+), 847 deletions(-)
git push

cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/issue8  #home
-----------------
* # update csl-orig on Cologne server
# Log in to Cologne server
cd csl-orig
git pull
cd ../csl-pywork/v02
# regenerate  displays for fri
sh generate_dict.sh fri  ../../FRIScan/2025/
-----------------
* # update this repo
cd /c/xampp/htdocs/sanskrit-lexicon/Frish/issues/
git add .
git commit -m "Latin to Cyrillic #8"
git push


========================================

