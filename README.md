# Heston_Calibation

Heston_Calibration.py calibrates the Heston Model using the Levenberg-Marquardt algoithm with COS-expansion calculation for the Heston model. Running the file will use pre-loaded historial data. It transforms prices to implied volatilities and calibrates onto the implied vols. Similar to conclusions in the literauture, the heston model struggles to price short dte options because it struggles to capture the implied vol smirk. Generally calibrate to data > 50-day expiries.

tools/Heston_COS_METHOD.py is a vectorised method of calculating European options for the heston model using cosine expansion. It is a robust method for fast Heston calculation and takes the cosine expansion of the whole integral of the fourier transform. It is vectorised along the different options AND vectorised along the summation. It is 300x faster than QuantLib's Python implementation FFT of the Heston, because we can truncate and use far less terms to converge (Typically only 64-100 terms vs 1,000 terms) 

tools/Levenberg_Marquardt.py is my own implementation of the Levenbrg-Marquardt Algorithm for calibrating the Heston model, and can calibrate all 5 parameters of the heston model. It converts the prices to implied volatilities and calibrated to implied volatilities. The damping factor is reduced based on the gain factor. Thus, the damping factor could still increase even if the step is accepted if the gain factor is too small.
