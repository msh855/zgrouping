# Finding Local Groupings of Time Series, ECML-PKDD 2022

## Introduction

This is an anonymous repository of Finding Local Groupings of Time Series, ECML-PKDD 2022.

## Dependencies

This application needs the latest version of the following packages (at the time of April 2022) and Python >= 3.7.

`numba`
`numpy`
`pyts`

## Creating local groupings 

Z-Grouping is a four-step framework for detecting local groupings of time series, by applying temporal abstraction and semigeometric tile detection.

The algorithm can be run by importing one method from this repository.

`from zgrouping.grouping import createLocalGroupings`

The algorithm receives the following parameters:
- matrices: event label matrix (see Step 1). This matrix can be created by applying `utils.createChannel`.
- alpha: a purity threshold (see Steps 1, 2).
- debug: print and debug option.
- accept: turn on the grouping quality validation function (Step 4).

These parameters are optional - and only available when the accept function is turned on (`accept = True`):
- c: a target global grouping (i.e., class label)
- metas: global grouping distribution (in general, **y** values of the dataset)
- eta: quality control score.

The algorithm returns the following values:
- R: a set of local groupings (Step 2)
- G: a set of associations (Step 3)

## Synthetic dataset generator

Synthetic dataset generator generates a dataset resembling the situation of shared local groupings among global groupings, having the local patterns we would like to retreive.

The generator can be run by importing one method from this repository.

`from zgrouping.syntheticGenerator import createSyntheticData`

The detailed explanation of the nature of the dataset is available in **the supplementary material**. This generator recieves the following parameters:
- c: number of global groupings
- tc: the number of member instances for each global grouping
- tl: length of each time series
- no_outliers: number of outliers
- outlier_size: outlier size
- amp: amplitudes
- lineranges: length of straight lines
- lineheights: height of straight lines

The function returns the following values:
- samples: a collection of the generated samples (**X**), with tc*c rows and l columns.
- metas: global grouping information for each sample (**y** - i.e., class labels).

The default value is set to the same ones used in the experiments of the paper.

The synthetic dataset we used is also available in this repository (in `datasets` directory).

## Utilities

The utils module provides useful functions for the algorithm.

- `utils.znorm`: apply time series z-normalization.
- `utils.createChannels`: create multiple channels for the multi level tiling (Steps 1-2).
- `utils.SAXify`: apply symbolic aggregate approximation to any numpy array.

## Example

An example of our profiling algorithm and how to use the synthetic generator is available in the Jupyter notebook `example.ipynb`.

This example goes through the whole process of generating local groupings and associations from the numpy dataset generated by the synthetic dataset generator.


## Experiment scripts

The experiment code used in the paper is available in this repository. Run `experimentScript.py` on the console to reproduce the result. 
The same parameters used in the paper are already applied. 

## Results

We provide various materials for the reproducibility of the experiment conducted in the paper.

- The main result of the experiment is available in the main context of this paper.
- The full result of the experiment is available as a supplementary material, which can be found in the submission form.
- The script to generate a whole result is provided in this repository (`experimentScript.py`).
  - The parameters are set to the ones used in the experiment.
- The python plots used in the paper are also available here (in `plots` directory).

## Datasets

The public COVID-19 dataset is collected from this repository from Johns Hopkins University:
https://github.com/CSSEGISandData/COVID-19

The S&P 500 stock dataset is collected from this repository:
https://www.kaggle.com/camnugent/sandp500

We put the original datasets (`stock_original.csv`, `stock_labels_original.csv`, `covid19original.csv`) and the processed ones (`covid.pickle`, `stock.pickle`) as well in this repository for reproducibility.
