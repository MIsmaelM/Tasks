# Spectral Analysis


This program will calculate absorption coefficients via the Beer-Lambert law from transmission spectra.


### Installation



|Operating System | Python Version | Numpy | Scipy | Matplotlib | Tkinter|
|Ubuntu 17.04|       3.11         |  1.13.1 | 0.19.1 |  2.0.2 | 8.6 |

### Running the code

1. First, you will run the code via the terminal with: `python Task_1.py`. 

2. Next, import the data used for analysis. The program will first ask for your raw dataset, followed by your background spectrum. Make sure to give a full path name


3. After importing these data files, the program will save the temperature and concentration of the mixture you are analyzing. The program will ask for both, and will store each answer in a separate txt file within the directory.

4. Once the data have been imported, the program will plot both data sets for user inspection (to make sure the data look okay) and ask which filtering method the user desires. The options are utilizing a [Savitzky-Golay filter](https://en.wikipedia.org/wiki/Savitzky–Golay_filter) (essentially a low-pass filter) or a Fast Fourier Transformation method (FFT) to manually remove unwanted frequencies. This filter step is used to remove any signal that might come form experimental methods. In the case of my project, there is a signal from reflection of sapphire windows in our laboratory setup. See [Protopapa 2015](https://arxiv.org/pdf/1503.00703.pdf) and [Grundy 2002](http://www.sciencedirect.com/science/article/pii/S0019103501967260) for more on this topic. I would recommend utilizing the FFT method, as this allows the user more control over the data being processed.

5. Once the user has determined a filtering method, the program will ask for further input for the user's choice. If the Savtizky-Golay filter was chosen, the user defines a window box size and a polynomial for the algorithm. See [the wikipedia article](https://en.wikipedia.org/wiki/Savitzky–Golay_filter) for more understanding of how it works. If the user chose the FFT option, a FFT is taken of the data, and the user hand selects the frequency to be cut out. The program listens for mouse clicks on the plot that is displayed, a left click will add a vertical line, a middle click will remove the nearest line, and a right click will tell the program that the user is satisfied with the selection and wants to proceed. In the gif provided one can see that the FFT is symmetric. The program will take the selection of frequencies (in the gif it is ~0.7 cm) and set them to zero, as well as their counterparts that are on the other side of the origin.


6. After the filtering process has been completed, the next step is to fit a continuum. This continuum defines where no absorption is occurring. The program will ask the user to zoom in on the region where the continuum wants to be fitted, and then will ask what order polynomial (linear, quadratic, etc) is to be used for creating the continuum. In the gif below I utilized a third order (cubic) but any fit is available to the user. I used a cubic fit for my work as it gave the most consistent results for my project. While the user clicks on the graph, the program fits a polynomial to all the data points that have been added to the graph. A left click adds a point, a middle click removes the nearest point, and a right click ends the collection.

7. After the continuum has been fit, the program asks the user to input the thickness of the cell used during spectra collection. This is because the absorption of light depends on the thickness of the cell chamber, via the [Beer-Lambert law](http://life.nthu.edu.tw/~labcjw/BioPhyChem/Spectroscopy/beerslaw.htm). The cell chamber used in my experiments was 2 cm, and thus a value of `2` will be entered. Finally, the program will generate absorption coefficients and display them for the user to inspect. Notice that not all of the spectrum can be relied upon for legitimate data, the end points (less than 90000 cm-1 and greater than 15000 cm-1) are not considered significant, so be sure not to include these values in calculations.

8. When finished viewing the plot, the user enters `y`, and the program closes. All of the data and plots generated during the program will be saved into the directory that was input at the beginning.


