RCIT
if random_seed: seed = np.random.choice(1000)
    else: seed = 5
    local_copy = X.copy()
    array = np.array(local_copy.transpose().dropna())
    dim, T = array.shape
    x_vals = array[x_]
    y_vals = array[y_]
    if z_ != None:
        z_vals = np.fastCopyAndTranspose(array[z_])
        rcot = rpy2.robjects.r['RCoT'](x_vals, y_vals, z_vals, seed = seed)
    else:
        rcot = rpy2.robjects.r['RCoT'](x_vals, y_vals, seed = seed)
    return float(rcot.rx2('p')[0])



x _||_ y | z
x _||_ y


import os
os.environ['R_HOME'] = '/Library/Frameworks/R.framework/Resources'
import rpy2
import statsmodels.api as sm
import rpy2.robjects
rpy2.robjects.r['options'](warn=-1)
from rpy2.robjects.packages import importr
import rpy2.robjects.numpy2ri
importr('RCIT')
rpy2.robjects.numpy2ri.activate()



linear test



def LinearIndependence(X,Y,Z=None, test= 'unconditional'):
    if test == 'unconditional':
        return(pearsonr(X,Y)[1])
    else:
        lm1 = list(sm.OLS(X,Z).fit().resid)
        lm2 = list(sm.OLS(Y,Z).fit().resid)
        return pearsonr(lm1, lm2)[1]






- simulate simple model (eg. chain)
- test conditional inndependence

X->Y->Z (chain)
X<-Z->Y (fork)
X->Z<-Y (collider)

X = np.random.normal(0,1,1000)

Y = X + Ny
Z = Y + Nz

