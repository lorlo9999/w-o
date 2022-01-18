#open the aligned images
hdulist = fits.open("stacked_final.fits")
dat = hdulist[0].data

#define needed parameters found on the photutils site
sigma_clip = SigmaClip(sigma=3.)
bkg_estimator = MedianBackground()

final_bc = [] #make empty list       
for i in range(27): 
    bkg = Background2D(dat[i], (50, 50), filter_size=(3, 3),sigma_clip=sigma_clip, bkg_estimator=bkg_estimator) # create the background estimation
    dat2 = dat[i]-bkg.background # subtract the estimated background
    final_bc.append(dat2) #append the refined images to the list
        
stacked_final_bc = np.stack(final_bc)   #stack the list of the images without background for convenient saving    
        
#save the new fits file in directory
hdu = fits.PrimaryHDU(stacked_final_bc)
hdul = fits.HDUList([hdu])
hdul.writeto("stacked_final_bc.fits", output_verify='ignore', overwrite=True)
print("The fits file containing all the images without background has been saved in the directory under the name: stacked_final_bc.fits ")
