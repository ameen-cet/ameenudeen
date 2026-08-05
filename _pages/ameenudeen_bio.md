I am a PhD student at the Department of Electrical Engineering, Indian Institute of Science (IISc), Bangalore, working with Dr. Sriram Ganapathy as part of the [LEAP Lab](http://leap.ee.iisc.ac.in). I also serve as an Assistant Professor in the Department of Electronics and Communication Engineering, College of Engineering Trivandrum.

**Research interests**

My work centers on representation learning for audio and speech, and on building small, efficient audio language models — including their end-to-end pre-training. This is complemented by a broader interest in information theory and communication, and grounded in a strong mathematical foundation in probability theory, linear algebra, and calculus for deep learning.

I have carried out complete self-supervised pre-training of audio foundation models such as HuBERT and SSAST. Two projects that reflect this work:

- [SmallALM](https://github.com/hrishikeshhpillai/smallALM) — a lightweight, 135M-parameter Audio Language Model that pairs a frozen self-supervised audio encoder with a compact language model (SmolLM2-135M) through a lightweight projector, aimed at showing that competitive audio understanding doesn't require billion-parameter models.
- [SSAST-MLM](https://github.com/ameen-cet/ssast_mlm) — a re-formulation of SSAST pre-training that replaces its two original self-supervised losses (masked patch classification and generation) with a single, unified masked-prediction objective in the style of HuBERT/BERT, turning spectrogram pre-training into a masked "language" modeling task over quantized audio tokens.

See the [CV](/cv/), [publications](/publications/), and [projects](/projects/) pages for more details.
