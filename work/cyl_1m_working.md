#title: A-scan from a metal cylinder in some air


@@ General Setup @@
#domain: 4.0 2.0 1.0
This^ is the bounds of the sim in meters.

#dx_dy_dz: 0.02 0.02 0.02
^Discrete chunks of the sim, also in meters

#time_window: 30e-9
In seconds of the sim^


@@ Materials @@
/#material: 3 0.01 1 0 my_sand
#material: 1 0 1 0 air 
/#material: 6 .10 1 0 wet_asphalt
/#material: 6 0 1 0 half_space
^epsilon, conductivity, mu, magnetic loss, name

/#box: 0 0 0 3 2 1 my_sand
#box: 0 0 0 3 2 1 air
Makes a box of a specified material^

/#sphere: 1.125 1.375 0.75 0.25 pec n
/#cylinder: 1.000 1.000 0.2 1.000 1.000 0.7 0.50 pec n
^this was totally 2m away, NOT 1m, which is why our reflection came in at 15 ns not 10 like it should at 1m!!!!
#cylinder: 2.000 1.000 0.200 2.000 1.000 0.700 0.500 pec n
/#cylinder: 1.125 2.325 0.1 1.125 2.375 0.8 0.50 wet_asphalt n
Makes a sphere at ^ with radius of .25m of 
a Perfect Electric Conductor and no dielectric smoothing


@@ EM Wave stuff @@
#waveform: ricker 1 6e8 my_pulse

/#hertzian_dipole: z 3.375 1.375 0.75 my_pulse
#hertzian_dipole: z 3.375 1.175 0.500 my_pulse
^ These make the pulse source and place it in the sim.
^also more centered now in z axis as is the rx

/#rx: 3.375 1.075 0.75
#rx: 3.375 0.875 0.500
/#rx: 3.375 1.075 0.75 Ex Ey Ez (only gives these parts, but still need to use --outputs Ez -fft for the graph and FFT)
^ Location of the receiver

#geometry_view: 0 0 0 4 2 1 0.02 0.02 0.02 big_cyl_halfspace n
^position, discretization, filename, and normal not fine so smaller filesize








Unused parameters:
Domain orignally was - 4.5 4.5 1.0

box was orignally 0 0 0 4 4.5 0.5 sand

box: 0 0 0 4 2 1 free_space
0 0 0.5 4.5 4.5 1 free_space
Makes open air above the land^

cylinder: 1.125 0 .5 1.125 2 .5 .125 pec y

material: 3 0 1 0 sand 










/#title: A-scan from a metal cylinder buried in a dielectric half-space
/#domain: 0.500 1.000 0.002
domain: 0.240 0.210 0.002
/#dx_dy_dz: 0.004 0.004 0.002
dx_dy_dz: 0.002 0.002 0.002
/#time_window: 30e-9
(was 3ns)

/#material: 6 0 1 0 half_space

/#waveform: ricker 1 1.5e9 my_ricker
/#hertzian_dipole: z 0.200 0.800 0 my_ricker
hertzian_dipole: z 0.100 0.170 0 my_ricker
/#rx: 0.300 0.190 0
rx: 0.140 0.170 0

/#box: 0 0 0 0.500 0.700 0.002 half_space
box: 0 0 0 0.240 0.170 0.002 half_space
/#cylinder: 0.120 0.700 0 0.120 0.700 0.002 0.030 pec
cylinder: 0.120 0.050 0 0.120 0.050 0.002 0.010 pec (forgot what original was)


/#geometry_view: 0 0 0 0.240 0.210 0.002 0.004 0.004 0.002 cylinder_half_space n


To run paraview go in terminal while in gprMax env, and go to ~/Downloads/Paraview..../bin and then use command ./paraview to open it. open another terminal if want to keep using paraview, or close and reopen after changes have been made



