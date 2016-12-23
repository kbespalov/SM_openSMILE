==============================================================================
mhealthx feature extraction software pipeline
==============================================================================<h1>
The `Child Mind Institute <http://childmind.org>`_ is developing mhealthx
as a general-purpose, open source software package to automate feature
extraction from sensor data.
`Arno Klein <http://binarybottle.com>`_ originally created mhealthx at
`Sage Bionetworks <http://sagebase.org>`_ to extract voice, accelerometry,
and touchscreen tapping features from mobile health research apps such as
`mPower <http://binarybottle.com/mpower/>`_, the Parkinson disease symptom tracking
app built on top of Apple's ResearchKit.
Behind the scenes, open source Python 3 and other languages run within a modular
Nipype pipeline framework on Linux (tested with Python 3.5 on Ubuntu 14.04).

:Release: |version|
:Date: |today|

Links:

.. toctree::
    :maxdepth: 1

    FAQ <faq.rst>
    license

- `GitHub <https://github.com/binarybottle/mhealthx>`_

- `CircleCI <https://circleci.com/gh/binarybottle/mhealthx/>`_

* :ref:`modindex`
* :ref:`genindex`

- In progress: `data-driven information visualizations <http://binarybottle.github.io/mhealthx/reports/index.html>`_

..
    1. Inputs
    2. Processing
    3. Outputs

------------------------------------------------------------------------------
_`Inputs`
------------------------------------------------------------------------------
All data are optionally accessed from Synapse tables in a project on synapse.org:

  - Voice: WAV files
  - Tapping: JSON files
  - Accelerometry: JSON files

------------------------------------------------------------------------------
_`Processing`
------------------------------------------------------------------------------
  - Run different feature extraction software packages on the input data.
  - Output features to new tables.

------------------------------------------------------------------------------
_`Outputs`
------------------------------------------------------------------------------
  - Tables


