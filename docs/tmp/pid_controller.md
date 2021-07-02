Module pid_controller
=====================
PID Control Class

Classes
-------

`Controller(args)`
:   PID Controller implementation.
    
    Parameters
    ----------
    args : dict
        The configuration dictionary parsed from yaml file.
    
    Attributes
    ----------
    _lon_ebuffer : deque
        A deque buffer that stores longitudinal control errors.
    
    _lat_ebuffer : deque
        A deque buffer that stores latitudinal control errors.
    
    current_transform : carla.transform
        Current ego vehicle transformation in CARLA world.
    
    current_speed : float
        Current ego vehicle speed.
    
    past_steering : float
        Sterring angle from previous control step.

    ### Methods

    `dynamic_pid(self)`
    :   Compute kp, kd, ki based on current speed.

    `lat_run_step(self, target_location)`
    :   Generate the throttle command based on current speed and target speed
        
        Parameters
        ----------
        target_location : carla.location
            Target location.
        
        Returns
        -------
        current_steering : float
        Desired steering angle value for the current step to
        achieve target location.

    `lon_run_step(self, target_speed)`
    :   Parameters
        ----------
        target_speed : float
            Target speed of the ego vehicle.
        
        Returns
        -------
        acceleration : float
            Desired acceleration value for the current step
            to achieve target speed.

    `run_step(self, target_speed, waypoint)`
    :   Execute one step of control invoking both lateral and longitudinal
        PID controllers to reach a target waypoint at a given target_speed.
        
        Parameters
        ----------
        target_speed : float
            Target speed of the ego vehicle.
        
        waypoint : carla.loaction
            Target location.
        
        Returns
        -------
        control : carla.VehicleControl
            Desired vehicle control command for the current step.

    `update_info(self, ego_pos, ego_spd)`
    :   Update ego position and speed to controller.
        
        Parameters
        ----------
        ego_pos : carla.location
            Position of the ego vehicle.
        
        ego_spd : float
            Speed of the ego vehicle
        
        Returns
        -------