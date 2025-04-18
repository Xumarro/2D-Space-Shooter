# 🚀 2D Space Shooter

A simple 2D space shooter game made using the Godot Engine. Inspired by classic arcade games.

## 🎮 Features
- Player movement and shooting
- Enemy waves
- Bullet collisions
- Score tracking
- Game over state

## 📅 Dev Log 04/11/2025
- Created game node and player node. Added "Quit" and "Reset" function using the ESC and R keys.
- Added player model of the ship, and not trying to debug why ship is not moving with current WASD key functions.
- Did input script into AI chat to furhter debug as I was not able to determine my issue, as nothing was producing in the Output screen.
- ![image](https://github.com/user-attachments/assets/fba91dbb-38f6-4e78-a329-08d61dd807d3)

- Was able to determine that no script was attached to my Player Node. Attached script, and player model was able to move using the WASD keys. Added a Print(direction) to show the Output, then later deleted as no longer needed.
- ![image](https://github.com/user-attachments/assets/e50df6b7-5381-4588-94d6-fcb22dc47140)

## 📅 Dev Log 04/18/2025
- Beginning to add laser shooting from player node.
- When testing laser, not able to get it to shoot upwards. Laswer is shooting downward under player.
- Was able to determine that in my coding, for global_position.y += speed * delta. Should be coded as global_position.y -= speed * delta. The y axis increases downward, so the "+" symbol was forcing the laser down, swiched to "-" and the laswer is shooting up.
- Created the laser to shoot from the muzzle of the space ship. Added a feature, to allow to change the cooldown of the laser shooting, as well as, a function to increase the speed of the laser being shot.
extends CharacterBody2D

signal laser_shot(laser_scene, location)

@export var speed = 300
@onready var muzzle = $Muzzle
var laser_scene = preload("res://Scenes/Laser.tscn")

var shoot_cooldown = 0.3
var time_since_last_shot = 0.0

func _process(delta):
	time_since_last_shot += delta

	if Input.is_action_pressed("shoot") and time_since_last_shot >= shoot_cooldown:
		shoot()
		time_since_last_shot = 0.0

func _physics_process(delta):
	var direction = Vector2(
		Input.get_axis("move_left", "move_right"),
		Input.get_axis("move_up", "move_down")
	)
	velocity = direction * speed
	move_and_slide()

func shoot():
	laser_shot.emit(laser_scene, muzzle.global_position)

- Adding an enemy! The enemy is now being called, and I am able to get the enemy on the screen, however, I am not able to get the enemy to move just yet.
- Was able to get the Enemy to begin moving down on the screen. Had to add a Script to the Enemy Scene. I was adding it to the Enemy Container, which did nothing for me.
- Now working on getting the enemy ship to "die" by the laser that my player ship shoots. Currently the enemy ship is passing over the top of the laser and player ship.
- Still unable to get laser and enemyship to collide thus causing the enemy ship to die.
