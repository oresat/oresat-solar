# Solar Simulator

# The Problem:  AKA Oh dear god why is everything so expensive



Normal incandescent solutions were too bulky to fit in our tiny vacuum chamber, they require a lot of power, and dissipate a whole lot of heat into the system.  LED solutions do exist, but they are insanely expensive. So-being the loveable open source rogues that we are- decided to build our own!

# The Design
















 # Component Calculations

 Vin = 56 V

 Vout = 48.2 V (worst case)

 switching frequency = fsw = 1 MHz

* Output Inductor
  * NOTE: Iripple must be at least 75 mA for reliable operation.  400 mA chosen to decrease size of inductor.
  * L = (Vout * (Vin - Vout) ) / (Iripple * Vin * fsw)
      = (48.2 * (56-48.2) )/ (.4 * (56) * (10^6) )
      = 170 uH
* Maximum Duty Cycle
  * D = Vout/Vin
      = 56/48.2
      = 86%
* Input Capacitance
  * Note: ΔVin is assuming a 5% ripple on Vin
  * Cin = (Iled * D * (1-D) )/(ΔVin * fsw)
        = (1 * .86 * .14)/(2.8*10^6)
        = 43 nF
* Dynamic resistance of LEDs
  * Rled = (ΔVled/ΔIled) * #LED
         = .5 * 15
         = 7.5 Ω
* Output Capacitance
  * Zcout = (Rled * ΔI) / (Iripple - ΔI)
          = (7.5 * .05) / (.2 - .05)
          = 2.5 Ω
  * Cout = 1 / (2 * π * fsw * Zcout)
         = 1 / (2 * π * 10^6 * 2.5)
         = .15 uF
* Power Dissipation
  * Psw = D * Rds * Iled^2
        = .86 * .28 * 1^2
        = .24 W
  * Piq = Vin * (400 * 10^-6 + (.002 * fsw) / 10^6)
        = 56 * (400 * 10^-6 +  (.002*10^6) / 10^6)
        = .13 W
  * Pac = .73 * 10^-9 * fsw * Vin^2 * Iled
        = .73 * 10^-9 * 10^6 * 56^2 * 1
        = 2.29 W
  * Ptotal = (Psw + Piq + Pac) * #LEDDrivers
           = (.24 + .13 + 2.29) * 3
           = 2.66 * 3
           = 7.98 W 