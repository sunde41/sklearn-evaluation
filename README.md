#sklearn-evaluation

[![Build Status](https://travis-ci.org/edublancas/sklearn-evaluation.svg?branch=master)](https://travis-ci.org/edublancas/sklearn-evaluation) [![PyPI version](https://badge.fury.io/py/sklearn-evaluation.svg)](https://badge.fury.io/py/sklearn-evaluation)

The cool kids way to evaluate scikit-learn models. Works with Python 2 and 3.

[Documentation here.](http://edublancas.github.io/sklearn-evaluation)

# Install  

```bash
pip install sklearn-evaluation
```

# Optional dependencies

If you want to use the reports module you need to install `mistune` and `tabulate` for the tables module

```bash
pip install mistune
pip install tabulate
```

#Usage

##`plot` module

Generate evaluation plots with a single function call.
```python
from sklearn_evaluation import plot

#code for data loading and model training

plot.confusion_matrix(y_true, y_pred, target_names=target_names)
```

![confusion matrix](examples/cm.png)

##`table` module

Generate good looking tables from your model results.

```python
from sklearn_evaluation import table

#code for data loading and training

table.feature_importances(model)
```

```
+-----------+--------------+-----------+
| name      |   importance |       std |
+===========+==============+===========+
| Feature 0 |    0.250398  | 0.0530907 |
+-----------+--------------+-----------+
| Feature 1 |    0.232397  | 0.0523836 |
+-----------+--------------+-----------+
| Feature 2 |    0.148898  | 0.0331814 |
+-----------+--------------+-----------+
| Feature 3 |    0.0553634 | 0.0128296 |
+-----------+--------------+-----------+
| Feature 8 |    0.05401   | 0.0122248 |
+-----------+--------------+-----------+
| Feature 5 |    0.053878  | 0.01289   |
+-----------+--------------+-----------+
| Feature 6 |    0.0525828 | 0.0130225 |
+-----------+--------------+-----------+
| Feature 9 |    0.0510197 | 0.0129436 |
+-----------+--------------+-----------+
| Feature 7 |    0.0509633 | 0.0117197 |
+-----------+--------------+-----------+
| Feature 4 |    0.0504887 | 0.012844  |
+-----------+--------------+-----------+
```

Also, running this in Jupyter will generate a pandas-like output.

##Using the OOP interface

A simplified API is available by packing the results of your estimator in the `ClassifierEvaluator` class.

```python
from sklearn_evaluation import ClassifierEvaluator

# code for data loading and model training

ce = ClassifierEvaluator(classifier, y_test, y_pred, y_score,
                         feature_list, target_names)

# this plots the confusion matrix
ce.confusion_matrix
```

## Generating reports

Generate reports using Markdown templates.

```python
 
 template = '''
            # Report
            {estimator_type}
            {date}
            {confusion_matrix}
            {roc}
            {precision_recall}
            '''

ce.generate_report(template, path='report.html')
```


The code above will generate a report [like this one.](http://htmlpreview.github.com/?https://github.com/edublancas/sklearn-model-evaluation/blob/master/examples/report.html)

Reports are self-contained, all images are included in the html file using [base64](https://en.wikipedia.org/wiki/Base64).


## Why?

Oftentimes during my projects I found myself copy pasting code with functions to evaluate my models, or even worse, coding ugly matplotlib lines to do pretty standard things. I love Jupyter, but having notebooks with the exact same plots, to just change the model being evaluated seems an overkill, that's the reason behind the markdown reports.

## What to expect next?

The project is still limited to the most common plots for evaluating classifiers, for now, I'll focus on that. I expect to add more plots/tables in the near future. If anyone is interested on contributing to add things for regression or clustering, drop me a line. 