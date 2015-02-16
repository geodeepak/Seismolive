# Installation of Anaconda Python/ObsPy for MESS

Please go to http://continuum.io/downloads, download and run the Anaconda installer for Python 2.7.

**Note:** On Mac/Linux, at the end of installation please confirm `"yes"` when asked if Anaconda Python should be prepended to your `PATH` environment variable.

After successful installation of the Anaconda Python Environment please install ObsPy:

**Windows**:
Click `Start` > `Programs` > `Anaconda` > `Anaconda Command Prompt`..

**Mac/Linux**:
Open a terminal..

Then type the following command:
```bash
easy_install obspy==0.9.2
```

After successful installation you should be able to start the IPython Notebook (from inside the Anaconda Command Prompt or Terminal)..

```bash
ipython notebook
```

The IPython Notebook should open in a new browser window or tab.

Click on `"New Notebook"`, type in the following commands and run the command cell (either click on arrow symbol or type CTRL-Enter).