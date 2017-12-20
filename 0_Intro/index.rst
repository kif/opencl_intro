.. raw:: html

   <!-- Patch landslide slides background color --!>
   <style type="text/css">
   div.slide {
       background: #fff;
   }
   </style>


Introduction to parallel programming
====================================

* Many-core CPU, GPU, FFPGA and accelerators are available on the market for >10 years
* They provide 10x more computing power than single threaded processor
* They need to programmed in a specific way using either:
 - Cuda (nvidia GPU only)
 - OpenCL (any-kind of devices)
 - OpenACC (not very open)
 - OpenMP 4+ (very recent)

We will focus on OpenCL using PyOpenCl


Credits: Pierre Paleo

----

What is a kernel in parallel programming?
=========================================

* A kernel is function executed on every point of a N-dimentional computational domain 
* The outer loop is *implicit*

Sequential code:
----------------
.. code-block:: C

    void vector_add(float* a, float* b, float* c, int count)
    {
        for (int i=0; i<count; i++)
        {
            c[i] = c[i] + b[i];
        }
    }
    
Parallel code:
--------------

.. code-block:: C

    kernel void vector_add(global float* a, global float* b, global float* c)
    {
        int i = get_global_id(0);
        c[i] = c[i] + b[i];
    }

