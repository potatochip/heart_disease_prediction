### Tree / Forest Challenges

You can examine the decision paths of an `sklearn` tree by generating `pydot` graphs as in the `sklearn` [documentation](http://scikit-learn.org/stable/modules/tree.html). It's sometimes tricky to get `pydot` working; see below for a possible install plan.


#### Challenge 1

For the house representatives data set, fit and evaluate a decision tree classifier. Examine the rules your tree uses.


#### Challenge 2

Fit and evaluate a decision tree classifier for your movie dataset. Examine the rules your tree uses.


#### Challenge 3 (Optional but recommended)

Tackle the [Titanic Survivors kaggle competition](https://www.kaggle.com/c/titanic-gettingStarted) with decision trees. Look at your splits; how does your tree decide?


### Installing pydot for the challenges:

Note: Uninstall pydot if you already installed it but it's not working

    pip uninstall pydot

Otherwise, you can start here:

    pip uninstall pyparsing

    pip install -Iv
    https://pypi.python.org/packages/source/p/pyparsing/pyparsing-1.5.7.tar.gz#md5=9be0fcdcc595199c646ab317c1d9a709

    pip install pydot

    brew install graphviz
