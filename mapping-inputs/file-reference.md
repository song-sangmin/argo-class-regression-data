# mapping-input reference files

inputs_path = '/Users/sangminsong/Documents/PROJECTS-PYTHON/CRUSOE-SOCarbon/x_localdata/working-vars/regression-inputs'

appl_path = '/Users/sangminsong/Documents/PROJECTS-PYTHON/CRUSOE-SOCarbon/x_localdata/argoclare-runs'

## synthetic 
synthetic_trainval:
(f'{inputs_path}/synthetic_max350km/combined_trainval_synthetic_pc8_gmm6_dbar500.csv')

synthetic_core (and uncertainty):
(f'{appl_path}/SYNTHETIC_max350km/synthetic_application_max350km_predictions_acc20261112.csv')


## real-world 
real_trainval:
(f'{inputs_path}/pHbias4pK014_max350km/combined_trainval_pc8_gmm6_dbar500.csv')

real_core: 
(f'{appl_path}/APPLICATION_pHbias4pK014_max350km/crusoe_application_pHbias4pK014_max350km_predictions_acc20261112.csv')


real_cv_uncertainty (stdev of calibrated error):
('/Users/sangminsong/Documents/PROJECTS-PYTHON/CRUSOE-SOCarbon/x_localdata/argoclare-runs/ALGORITHMS_pHbias4pK014_max350km/crusoe_RFR_rfr_full_pHbias4pK014_max350km_outercvErrors_acc20261112.csv')

real_test_uncertainty:
('/Users/sangminsong/Documents/PROJECTS-PYTHON/CRUSOE-SOCarbon/x_localdata/argoclare-runs/APPLICATION_pHbias4pK014_max350km/crusoe_application_pHbias4pK014_max350km_testPredictions_acc20261112.csv')

## uncertainties
platform = real_output['platform']
real_output['uncertainty'] = np.select(
    [platform.eq('socatv2025'),
     platform.eq('coreArgo'),
     platform.eq('bgcArgo')],
    [5.0,
     21.5,
     0.027 * real_output['pco2_ocean']],
    default=np.nan,
)
