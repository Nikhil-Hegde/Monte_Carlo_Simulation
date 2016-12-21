# Monte_Carlo_Simulation
from scipy import special
import numpy as np

def pdf(x,y,z,s,t,l1,l2):

	#PDF for domain z>0
	def left_function(y,z,s,t,l1,l2):
    	return l1*(l1*y+z)**(s-1)/(special.gamma(s))*np.exp(-l1*(y+z))*l2*(l2*y)**(t-1)/(special.gamma(t))*np.exp(-l2*y)

	#PDF for domain z<0
	def right_function(x,z,s,t,l1,l2):
    	return l1*(l1*x)**(s-1)/(special.gamma(s))*np.exp(-l1*x)*l2*(l2*(x-z))**(t-1)/special.gamma(t)*np.exp(-l2*(x-z))	

	if z < 0:
		return left_function(y,z,s,t,l1,l2)
	else:
		return right_function(x,z,s,t,l1,l2)

dens = pdf(linspace(-0.01,-0.0001,100),linspace(0.0001,0.01),0.1,1,1,400,547)
plot(dens)
