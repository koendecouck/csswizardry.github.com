---
layout: post
title: "3D Printed Brain"
meta: "3d-printed-brain"
permalink: /case-studies/20140809-3dprintedbrain/
next-case-study-title: "3D printed MRI data"
next-case-study-url: /case-studies/20140809-3dprintedbrain/
hide-hire-me-link: true
---
MeshLab, 3D modeling

As a summer pet project, I explored the possibility of transforming medical MRI data into 3D printed model replicas. 

<p>Models have important applications in medical research or when training medical students. Both for convenience and reasons of awesome, I decided to experiment using my own brain. Convenient, because I participated in a university neurological study a few years ago to which I still held the scan.</p>

<p style="text-align: left;"><b style="line-height: 1.5em;">Problem description</b></p>
<p style="text-align: left;"><b style="line-height: 1.5em;"></b><a href="http://science.howstuffworks.com/mri.htm">Magnetic resonance imaging<span style="line-height: 1.5em;"> (</span>MRI</a><span style="line-height: 1.5em;"><a href="http://science.howstuffworks.com/mri.htm">)</a> is a medical imaging technique used in radiology to investigate the physiology of the body in both health and disease. MRI scanners use strong magnetic fields and radiowaves to form 3D images of the body. The technique is widely used in hospitals for medical diagnosis, staging of disease and for follow-up without exposure to ionizing radiation. The technique has been used for about thirty years, long before the development of 3D printers. Not surprisingly, the two use very different imaging standards to record 3D information. <em>DICOM (</em><em>Digital Imaging and Communications in Medicine)</em> is a standard for handling, storing, printing, and transmitting information in medical imaging. <em>STL (Stereolithography)</em> is a file format native to the stereolithography CAD software created by 3D Systems. STL is widely used for rapid prototyping and computer-aided manufacturing. It would be interesting to tie those together: the ability to print organs could help in exploring a medical diagnosis. It could limit the number of scans to the patient and be of significant value for medical training.</span></p>

<p><strong>Method</strong></p>
<p><strong>The main steps involved were:</strong></p>
<ol>
	<li>Converting sliced DICOM raw data into the STL file format</li>
	<li>Editing the model in a 3D editor</li>
	<li>Smoothen edges, build raft and supports</li>
	<li>3D printing a solid object</li>
</ol>
<p><strong>1. Converting sliced DICOM raw data into the STL file format</strong></p>

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000000.png" alt="">
  <figcaption>The original fMRI scan<a href="/case-studies/20140809-3dprintedbrain/20140809-000000.png">View full size/quality (172KB).</a></figcaption>
</figure>
The original fMRI scan.

To start you need a high-quality T1-weighted anatomical MRI scan of your head. MRI data is typically stored in the DICOM format, often accompanied by an autorun exploration tool (Windows only) that allows you to visually inspect individual slices.

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000001.png" alt="">
  <figcaption>Multiplanar visualization of different tissues (bone, facial muscles, epidermis). The last shot has a teal colored filter applied showing the direction of the magnetic field. Made using InVesalius 3.<a href="/case-studies/20140809-3dprintedbrain/20140809-000001.png">View full size/quality (172KB).</a></figcaption>
</figure>

<p><a href="http://svn.softwarepublico.gov.br/trac/invesalius">InVesalius 3</a> is an open source medical application for Windows and Linux, allowing you to import the DICOM file folder and export it again an STL file. It also comes with a number of rough pre-set filters (see photo). You could choose to filter out bone and fat tissue or just export everything. It's fast and easy. Another good open source alternative is the <a href="https://surfer.nmr.mgh.harvard.edu/fswiki">FreeSurfer package for fmri data</a> (linux). Freesurfer is a lot more powerful, but also quite technical. Only use it if you're comfortable working from the terminal. I used this package on a second go and found myself frequently referring to the documentation. You will want to do an automatic reconstruction ('recon-all'), and convert the generated surfaces 'rh.pial' and 'lh.pial' to STL ('mris_convert'). The real work of filtering however has to be done manually, which will the next step.</p>

<p><strong>2. Editing the model in a 3D editor</strong></p>

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000002.png" alt="">
  <figcaption>Cleaning up the final model using MeshLab.<a href="/case-studies/20140809-3dprintedbrain/20140809-000002.png">View full size/quality (172KB).</a></figcaption>
</figure>

<p>I used <a href="http://meshlab.sourceforge.net/">MeshLab</a> for this, which is free and works across platforms. MeshLab is an advanced 3D mesh processing software system which is well known in the more technical fields of 3D development and data handling. If you're willing to spend some money I can also recommend Rhino 3D. <a href="http://www.rhino3d.com/">Rhino 3D</a> is a stand-alone, commercial 3-D modeling software application based on a mathematical model called NURBS (non-uniform rational B-spline), which is adept at producing curves and surfaces in computer graphics. It has a relatively low learning-curve while still being fairly cheap.</p>

<p>I decided to go with MeshLab, which has a clean and very straightforward interface. It has in-build filters, however I recommend removing sections through drag and drop selection of sections on the outer skull and deleting them. The human brain essentially floats in a watery space in the skull called the subarachnoid space. On an MRI scan this shows up as empty space between the skull and the actual brain. Select the outer edge, delete, rotate and repeat. You will probably end up with a lot of loose, disconnected skull fragments after a while. MeshLab has a selection tool that will automatically highlight those for you, which makes it easier to clean up. Once you're done you should have something resembling the picture above. If you decided to use FreeSurfer in the previous phase there shouldn't be any need to edit content.</p>

<p><strong>3. Smoothen edges, build raft and supports</strong></p>

<p>Still in MeshLab, consider downsampling the number of faces for the mesh, using Quadratic Edge Collapse Decimation. This tool can be found in the filter menu under remeshing, simplification and reconstruction. The number of faces corresponds to the resolution of the mesh. Choose a lower amount to ease up the work on your computer and printer. You could also perform another simplification operation called a Poisson reconstruction when you're done. This will make the gyri and sulci of the cortex look more spheroid by smoothing edges on the model. The level can be manipulated for a hard or soft effect. Like the last tool the Poisson reconstruction tool can be found under remeshing, simplification and reconstruction. Save the model when you're done.</p>

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000003.png" alt="">
  <figcaption>Print preview with MakerWare: rotation, scale and adding supports.<a href="/case-studies/20140809-3dprintedbrain/20140809-000003.png">View full size/quality (172KB).</a></figcaption>
</figure>

<p>Finally you have the choice to move, rotate, scale, and otherwise transform the imported model. The <a href="http://www.makerbot.com/desktop">MakerWare</a> interface is a simple STL/OBJ positioning tool to accomplish this for the Makerbot Replicator. It's similar to checking a print preview on your run-of-the-mill printer. Scale the model to an appropriate size for your 3D printer. Adding a raft and supports can be done through a simple check box option in the menu. When you're ready send it of to the printer.</p>

<p><strong>4. printing a solid object</strong></p>

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000004.png" alt="">
  <figcaption>Printing a so-called 'raft' first, which makes for a more stable surface to print on.<a href="/case-studies/20140809-3dprintedbrain/20140809-000004.png">View full size/quality (172KB).</a></figcaption>
</figure>

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000005.png" alt="">
  <figcaption>Nearly finished printing. Note the added tendrils forming the support structure.<a href="/case-studies/20140809-3dprintedbrain/20140809-000005.png">View full size/quality (172KB).</a></figcaption>
</figure>

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000006.png" alt="">
  <figcaption>Carefully removed the supports.<a href="/case-studies/20140809-3dprintedbrain/20140809-000006.png">View full size/quality (172KB).</a></figcaption>
</figure>

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000007.png" alt="">
  <figcaption>Final result, holding a model replica of my brain.<a href="/case-studies/20140809-3dprintedbrain/20140809-000007.png">View full size/quality (172KB).</a></figcaption>
</figure>

<p><strong>Conclusion</strong></p>

<figure>
  <img src="/case-studies/20140809-3dprintedbrain/20140809-000008.png" alt="">
  <figcaption>With recent advances in the cost and flexibility of 3D printing technology, the printing of medical scanned objects has the potential to become much more commonplace.<a href="/case-studies/20140809-3dprintedbrain/20140809-000008.png">View full size/quality (172KB).</a></figcaption>
</figure>

---

{% include promo-next.html %}
