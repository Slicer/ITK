What is this project ?
----------------------

This project is **NOT** the official ITK repository.

It is a fork of ITK sources hosted at https://github.com/InsightSoftwareConsortium/ITK.

It is used as staging area to maintain and test patches that will be contributed back to the
official repository.


What is the branch naming convention ?
--------------------------------------

Each branch is named following the pattern `slicer-vY.Y.Z-YYYY-MM-DD-SHA{7}`

where:

* `vX.Y.Z` is the version of the forked project
* `YYYY-MM-DD` is the date of the last official commit associated with the branch.
* `SHA{7}` are the first seven characters of the last official commit associated with the branch.

For more details, see https://www.slicer.org/wiki/Documentation/Nightly/Developers/ProjectForks


How to update the version of ITK ?
----------------------------------

1. Clone this repository and add a remote to the official project

```
git clone git://github.com/Slicer/ITK
cd ITK
git remote add upstream git://github.com/InsightSoftwareConsortium/ITK
git fetch upstream
```

2. Create a new branch following the convention

```
# Extract version from https://github.com/InsightSoftwareConsortium/ITK/blob/master/CMakeLists.txt
XYZ=$(cat CMakeLists.txt | grep ^set\(ITK_VERSION | sed -re 's/^set\(ITK_VERSION_[A-Z]+ \"(.+)\"\)/\1/' | perl -pe 'chomp if eof' | tr '\n' '.')
echo "XYZ [${XYZ}]"

DATE=$(git show -s --format=%ci upstream/master | cut -d" " -f1)
echo "DATE [${DATE}]"

SHA=$(git show -s --format=%h upstream/master)
echo "SHA [${SHA}]"

BRANCH=slicer-v${XYZ}-${DATE}-${SHA}
echo "BRANCH [${BRANCH}]"

git checkout -b ${BRANCH}  ${SHA}
```

3. Cherry-pick the Slicer specific commits from last branch. Resolve conflict as needed.

4. To **test the changes**, locally rebuild ITK, SlicerExecutionModel, SimpleITK, CTK and Slicer.

5. Publish the branch. (directly in this repo if you have push rights, or on a fork)

6. Update Slicer ITK external project and submit a pull request.


How to be granted push rights ?
-------------------------------

Ask on https://discourse.slicer.org/


Questions
---------

If you have questions, see https://discourse.slicer.org/
