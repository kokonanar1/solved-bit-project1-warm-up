Download Link: https://assignmentchef.com/product/solved-bit-project1-warm-up
<br>
<strong>project 1: warm up</strong>

<strong>task 1.1: acquaint yourself with python for pattern recognition </strong>First of all, download the file

<h1>whExample.py</h1>

from the Google site that accompanies the lecture; second of all, retrieve the file

<h1>whData.dat</h1>

and run the above script. It should plot sizes vs. weights of students from an earlier course on pattern recognition<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>.

Note that two students did not want to disclose their weight. This provides us with an opportunity to deal with missing data. In the plot produced by the script, these data points appear with negative weights (they are <em>outliers</em>).

For starters, try to figure out a way of plotting the data without the outliers, that is, figure out how to plot only those data for which both measurements are positive.

<strong>task 1.2: fitting a Normal distribution to 1D data</strong>

Now consider only the data on body sizes, i.e. consider the 1D array of data containing the size information.

Compute the mean and standard deviation of this sample, plot the data and a normal distribution characterizing its density. Your result should resemble the following figure:

<strong>task 1.3: fitting a Weibull distribution to 1D data </strong>Download the file

<h1>myspace.csv</h1>

which contains Google Trends data that indicate how global interest in the query term <em>“myspace” </em>evolved over time. Read the data in the second column of the file and remove leading zeros! Store the remaining entries in an array <em>h </em>= [<em>h</em><sub>1</sub><em>,h</em><sub>2</sub><em>,…,h<sub>n</sub></em>] and create an array <em>x </em>= [1<em>,</em>2<em>,…,n</em>].

Now, fit a Weibull distribution to the histogram <em>h</em>(<em>x</em>). The probability density function of the Weibull distribution is given by

where <em>κ </em>and <em>α </em>are a shape and scale parameter, respectively. Unlike in the case of the Normal distribution, maximum likelihood estimation of the parameters of the Weibull distribution is more involved.

Given a data sample, the log-likelihood for the parameters of

the Weibull distribution is

<em>.</em>

Deriving <em>L </em>with respect to <em>α </em>and <em>κ </em>leads to a coupled system of partial differential equations for which there is no closed form solution. Therefore, resort to Newton’s method for simultaneous equations and compute

where the entries of the gradient vector and the Hessian matrix amount to

<strong> note:</strong>

You are given a histogram <em>h</em>(<em>x</em>) where <em>h<sub>j </sub></em>counts the number of observations of a value <em>x<sub>j</sub></em>. The MLE procedure outlined above assumes that you are given individual observations <em>d<sub>i</sub></em>. That is, it assumes as input <em>h</em><sub>1 </sub>times a value of <em>x</em><sub>1</sub>, <em>h</em><sub>2 </sub>times a value of <em>x</em><sub>2</sub>, etc. In other words, <em>d</em><sub>1 </sub>= <em>x</em><sub>1</sub><em>,d</em><sub>2 </sub>=

<em>x</em>1<em>,…d</em><em>h</em>1 = <em>x</em>1<em>,…,d</em><em>h</em>1+1 = <em>x</em>2<em>,…,d</em><em>h</em>1+<em>h</em>2 = <em>x</em>2<em>,…</em>

That is, you have to turn the histogram into a (large) set of numbers for the procedure to work. But there also is a more elegant solution, can see and implement it?

Be ambitious! Analyze why the above approach is unnecessarily cumbersome and come up with a much faster approach.

If you initialize <em>κ </em>= 1 and <em>α </em>= 1 and run the estimation procedure for about 20 iterations, then which values do you obtain for <em>κ </em>and <em>λ</em>?

When you plot the histogram and a correspondingly scaled version of the fitted distribution, your result should resemble this figure:

<table width="382">

 <tbody>

  <tr>

   <td width="160">     Google data</td>

   <td width="84"> </td>

   <td width="81"></td>

   <td width="57">Weibull fit</td>

  </tr>

 </tbody>

</table>

<strong> note:</strong>

If you want to impress your professor, then additionally figure out how to use the function scipy.integrate.odeint to solve this task. Again, be ambitious and search the Web for tutorials . . .

<strong>task 1.4: drawing unit circles</strong>

In the lecture we discussed <em>L<sub>p </sub></em>norms for R<em><sup>m </sup></em>and saw that, for different <em>p</em>, the corresponding unit spheres may look different. For instance, the following examples show unit circles in R<sup>2</sup>:

Consider the <em>L<sub>p </sub></em>norm for and plot the corresponding R<sup>2 </sup>unit circle.

Is this really a norm or not? Discuss why or why not!

<strong>task 1.5: estimating the dimension of fractal objects in an image </strong>In the lecture we discussed the use of least squares for linear regression; here we consider a neat practical application of this technique. <em>Box counting </em>is a method to determine the fractal dimension of an object in an image. For simplicity, let us focus on square images whose width and height (in pixels) are an integer power of two, for instance

<em>w </em>= <em>h </em>= 2<em><sup>L </sup></em>= 512           ⇔          <em>L </em>= 9

Given such an image, the procedure involves three main steps:

<ol>

 <li>apply an appropriate binarization procedure to create a binary image in which foreground pixels are set to 1 and background pixels to 0</li>

</ol>

→

<ol start="2">

 <li>specify a set <em>S </em>of scaling factors 0 <em>&lt; s<sub>i </sub>&lt; </em>1, for instance</li>

</ol>

and, for each <em>s<sub>i </sub></em>∈ <em>S</em>, cover the binary image with boxes of size <em>s<sub>i </sub>w</em>× <em>s<sub>i </sub>h </em>and count the number <em>n<sub>i </sub></em>of boxes which contain at least one foreground pixel

<ul>

 <li>··</li>

</ul>

<ol start="3">

 <li>plot log<em>n<sub>i </sub></em>against and fit a line</li>

</ol>

to this data; the resulting estimate for <em>D </em>is the fractal dimension we are after.

In other words, the problem of estimating <em>D </em>is a simple linear regression problem that can of course be tackled using least squares.

Now, implement the box counting method and run it on the two test images tree-2.png and lightning-3.png.

What fractal dimensions do you obtain? Which object has the higher one, the tree or the lightning bolt?

<strong> note:</strong>

If you use the following snippet

<table width="518">

 <tbody>

  <tr>

   <td width="518">import numpy as np import scipy.misc as msc import scipy.ndimage as imgdef foreground2BinImg(f):d = img.filters.gaussian_filter(f, sigma=0.50, mode=’reflect’) –  img.filters.gaussian_filter(f, sigma=1.00, mode=’reflect’)d = np.abs(d) m = d.max() d[d&lt; 0.1*m] = 0 d[d&gt;=0.1*m] = 1return img.morphology.binary_closing(d)imgName = ’lightning-3’f = msc.imread(imgName+’.png’, flatten=True).astype(np.float) g = foreground2BinImg(f)</td>

  </tr>

 </tbody>

</table>

to read and binarize an image, then the outcome of the box counting procedure should be deterministic. I.e. every team using this snippet should obtain the same results and these results should be the same as those your professor got. Teams getting different results can rest assured they made a mistake. Try not to be one of these teams

<a href="#_ftnref1" name="_ftn1">[1]</a> Depending on what version of python you are using the script may or may not work properly. If it does not work properly, see this as a learning opportunity and fix the errors yourself.