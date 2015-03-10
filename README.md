# ROI
Code to define a ROI

% March 2014 edited to define 1 region in embryo data
% April 2014 added so2_calc function
% V4 May 2014 - rewrote to define segment before analysis
% V5 - minimal changes to sync with the work optimizing the run time (reshaping the data to 1D) 

    clear Region;

    %///user defined\\\
    %e.g. [1 1]
    Region(1).Frame = [1]; %manually enter in frames of interest for ROI analysis
    Region(2).Frame = [1];
    Region(3).Frame = [1];
            
    cfiles = dir('*V7_Conc.mat');

   for ifile = 1:size(cfiles,1)
  % for ifile = 1:1 for debugging
        fname = cfiles(ifile).name;
        fnameBase =  cfiles(ifile).name(1:end-15);
        fnameUS = [fnameBase 'US.mat'];
        fnamePA = [fnameBase 'sPA.mat'];
        load (fnamePA);
        load (fnameUS);

        frame_sel = Region(ifile).Frame;
       
        for iframe = 1:size(frame_sel,2) %selected frame
           
           figure;image_dbgsc_hot(US_small(:,:,frame_sel(iframe)),0,size(US_small,1),PA(:,:,1,frame_sel(iframe)),0,1000,100,1,size(PA,1),1,size(PA,2),0); 
           Region(ifile).ROI(:,:,iframe) = roipoly;

        end
    end
    save(['ROI'], 'Region')
