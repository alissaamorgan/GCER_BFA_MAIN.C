# GCER_BFA_MAIN.C
#include <kipr/botball.h>
#include <ARM.h>
int main()
{
	create_connect();
	create_full();

	set_servo_slow(shoulder,shoulder_start_position);
	set_servo_slow(wrist, 322);
	set_servo_slow(claw, claw_closed);
	create_drive_direct(-200, -200);
	msleep(500);
	create_stop();
	msleep(3000);//take this out after wait for light is functional
	//wait_for_light(0);
	create_drive_direct(100,100);//set up palms
	msleep(400);
	create_stop();
	move_claw(claw_open);
	move_wrist_to(wrist_for_front_pickup);
	msleep(300);
	shoulder_doze();//don't touch above
	create_drive_direct(60, 60);
	msleep(900);
	claw_slow_close();
	create_stop();
	create_drive_direct(-300,-300);
	msleep(700);
	move_claw (claw_open);
	create_forward(1400);//perfect
	claw_slow_close();
	create_backward(1500);//backs up into wall for first half of squareup
	create_forward(200);//moves away from wall for second half of squareup
	create_drive_direct(-200, 200);//turning for second half of squareup
	msleep(800);
	create_stop();
	doze_to_dump();//move arm from doze to dump
	create_drive_direct(50, 100);
	msleep(1000);//good but not
	create_stop();
	create_backward(400);//perform second half of squareup
	//at this point, Create is squared up in starting box, facing tram, with poms in dump position bucket
	create_forward(4000);//experimental travel numbers to get claw to tram...change and add to this to get in position to make the next CCW turn
	
	/*CCW(1000);
	create_backward(600);
	CW(100);
	create_forward2(1800);
	msleep(500);
	CW(640);
	create_backward(2000);
	perfect_turn();
	//set_servo_position(claw,900);
	create_forward3(600);
	
	claw_to_delivery();
	msleep(100);
	create_forward3(2000);
	create_stop();
	wrist_to_delivery();
	claw_to_delivery2();
	//place movement functions here
	//dump_to_doze();
	//place movement functions here
	frisbee_approach_positions();
	msleep(1000);
	pick_frisbee_up();*/
	disable_servos();
	create_safe();
	create_disconnect();
	return 0;
}
