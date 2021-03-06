# MODELO-SIR
Aplicación de métodos numéricos para su solución 
import numpy as np
from matplotlib import pyplot as plt

h = 1

r=1/2
a=1/3

t=np.linspace(1,200,200)

Sa,Ia,Ra=[1],[0.00000127],[0]
Sb,Ib,Rb=[1],[0.00000127],[0]
Sc,Ic,Rc=[1],[0.00000127],[0]
Sd,Id,Rd=[1],[0.00000127],[0]
Se,Ie,Re=[1],[0.00000127],[0]
Sf,If,Rf=[1],[0.00000127],[0]
Sg,Ig,Rg=[1],[0.00000127],[0]
Sh,Ih,Rh=[1],[0.00000127],[0]

# euler
for i in t[1:]:
    Sa1=Sa[-1]-r*Sa[-1]*Ia[-1]*h
    Ia1=Ia[-1]+(r*Sa[-1]*Ia[-1]-a*Ia[-1])*h
    Ra1=Ra[-1]+(a*Ia[-1])*h
    Sa.append(Sa1)
    Ia.append(Ia1)
    Ra.append(Ra1)

# Euler implícito 
for j in t[1:]:
    Ib1=Ib[-1]/(1-(h*r*Sb[-1])+a*h)
    Sb1=Sb[-1]/(1+r*h*Ib[-1])
    Rb1=Rb[-1]+h*(a*Ib[-1])
    Sb.append(Sb1)
    Ib.append(Ib1)
    Rb.append(Rb1)

#heun
for l in t[1:]:
    k1S = -r*Sc[-1]*Ic[-1]
    k1I = r*Sc[-1]*Ic[-1]-a*Ic[-1]
    k1R = a*Ic[-1]
    k2S = -r*(Sc[-1] + 2/3*k1S*h)*(Ic[-1] + 2/3*k1I*h)
    k2I = r*(Sc[-1] + 2/3*k1S*h)(Ic[-1] + 2/3*k1I*h)-a(Ic[-1] + 1/2*k1I*h)
    k2R = a*(Ic[-1] + 2/3*k1I*h)
    Sc1 = Sc[-1] + (h/4)*(k1S+3*k2S)
    Ic1 = Ic[-1] + (h/4)*(k1I+3*k2I)
    Rc1 = Rc[-1] + (h/4)*(k1R+3*k2R)  
    Sc.append(Sc1)
    Ic.append(Ic1)
    Rc.append(Rc1)  
        
#Modificado
for n in t[1:]:
    k1S = -r*Sd[-1]*Id[-1]
    k1I = r*Sd[-1]*Id[-1]-a*Id[-1]
    k1R = a*Id[-1]
    k2S = -r*(Sd[-1] + k1S*h)*(Id[-1] + k1I*h)
    k2I = r*(Sd[-1] + k1S*h)(Id[-1] + k1I*h)-a(Id[-1] + k1I*h)
    k2R = a*(Id[-1] + k1I*h)
    Sd1 = Sd[-1] + (h/2)*(k1S+k2S)
    Id1 = Id[-1] + (h/2)*(k1I+k2I)
    Rd1 = Rd[-1] + (h/2)*(k1R+k2R)  
    Sd.append(Sd1)
    Id.append(Id1)
    Rd.append(Rd1)  
        
#Punto medio
for p in t[1:]:
    k1S = -r*Se[-1]*Ie[-1]
    k1I = r*Se[-1]*Ie[-1]-a*Ie[-1]
    k1R = a*Ie[-1]
    k2S = -r*(Se[-1] + k1S*(h/2))(Ie[-1] + k1I(h/2))
    k2I = r*(Se[-1] + k1S*(h/2))(Ie[-1] + k1I(h/2))-a*(Ie[-1] + k1I*(h/2))
    k2R = a*(Ie[-1] + k1I*(h/2))
    Se1 = Se[-1] + (h)*(k2S)
    Ie1 = Ie[-1] + (h)*(k2I)
    Re1 = Re[-1] + (h)*(k2R)  
    Se.append(Se1)
    Ie.append(Ie1)
    Re.append(Re1)    
    
#runge-kutta
for n in t[1:]:
    k1S = -r*Sf[-1]*If[-1]
    k1I = r*Sf[-1]*If[-1]-a*If[-1]
    k1R = a*If[-1]
    k2S = -r*(Sf[-1] + 1/2*k1S*h)*(If[-1] + 1/2*k1I*h)
    k2I = r*(Sf[-1] + 1/2*k1S*h)(If[-1] + 1/2*k1I*h)-a(If[-1] + 1/2*k1I*h)
    k2R = a*(If[-1] + 1/2*k1I*h)
    k3S = -r*(Sf[-1] + 1/2*k2S*h)*(If[-1] + 1/2*k2I*h)
    k3I = r*(Sf[-1] + 1/2*k2S*h)(If[-1] + 1/2*k2I*h)-a(If[-1] + 1/2*k2I*h)
    k3R = a*(If[-1] + 1/2*k2I*h)
    k4S = -r*(Sf[-1] + k3S*h)*(If[-1] + k3I*h)
    k4I = r*(Sf[-1] + k3S*h)(If[-1] + k2I*h)-a(If[-1] + 1/2*k2I*h)
    k4R = a*(If[-1] + k3I*h)
    Sf1 = Sf[-1] + (h/6)*(k1S+2*k2S+2*k3S+k4S)
    If1 = If[-1] + (h/6)*(k1I+2*k2I+2*k3I+k4I)
    Rf1 = Rf[-1] + (h/6)*(k1R+2*k2R+2*k3R+k4R)
    Sf.append(Sf1)
    If.append(If1)
    Rf.append(Rf1)   

#trapecio
for z in t[1:]:
    Sh1=Sh[-1]*(1-(h/2)*r*Ih[-1])/(1+(h/2)*r*Ih[-1])
    Ih1=(Ih[-1](1+(h/2)(r*Sh[-1]-a)))/(1-(h/2)*(r*Sh[-1]-a))
    Rh1=Rh[-1]+h*(a*Ih[-1])
    Sh.append(Sh1)
    Ih.append(Ih1)
    Rh.append(Rh1)

fig, ax = plt.subplots()
plt.plot(t,Sa,label='Euler explícito')
plt.plot(t,Sb,label='Euler implícito')
plt.plot(t,Sc,label='Heun')
plt.plot(t,Sd,label='Euler modificado')
plt.plot(t,Se,label='Punto medio')
plt.plot(t,Sf,label='Runge-Kuta 4to orden')
plt.plot(t,Sh,label='Trapecio')
plt.legend()
plt.xlabel('t (días)')
plt.ylabel('s(t)')
plt.title('B = 1/2'+','+' G = 1/3')
plt.show()
fig, ax = plt.subplots()
plt.plot(t,Ia,label='Euler explícito')
plt.plot(t,Ib,label='Euler implícito')
plt.plot(t,Ic,label='Heun')
plt.plot(t,Id,label='Euler modificado')
plt.plot(t,Ie,label='Punto medio')
plt.plot(t,If,label='Runge-Kuta 4to orden')
plt.plot(t,Ih,label='Trapecio')
plt.legend()
plt.xlabel('t (días)')
plt.ylabel('i(t)')
plt.title('B = 1/2'+','+' G = 1/3')
plt.show()
fig, ax = plt.subplots()
plt.plot(t,Ra,label='Euler explícito')
plt.plot(t,Rb,label='Euler implícito')
plt.plot(t,Rc,label='Heun')
plt.plot(t,Rd,label='Euler modificado')
plt.plot(t,Re,label='Punto medio')
plt.plot(t,Rf,label='Runge-Kuta 4to orden')
plt.plot(t,Rh,label='Trapecio')
plt.legend()
plt.title('B = 1/2'+','+' G = 1/3')
plt.xlabel('t (días)')
plt.ylabel('r(t)')
plt.show()
