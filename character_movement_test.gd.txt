extends Node

func _ready():
    # Run the tests
    test_movement()

func test_movement():
    # Create a test environment
    var character = preload("res://path_to_your_character_scene.tscn").instance()
    add_child(character)

    # Assuming your character starts at a specific position, you may want to check that here.

    # Simulate inputs (you might need to adjust these according to your actual input mappings)
    Input.fake_input("ui_right", true)
    yield(get_tree(), "idle_frame")
    
    # Check if the character is moving right
    assert(character.velocity.x > 0, "Character should move right when pressing 'ui_right'")

    # Simulate releasing the input
    Input.fake_input("ui_right", false)
    yield(get_tree(), "idle_frame")
    
    # Check if the character stops moving
    assert(character.velocity.x == 0, "Character should stop moving when releasing 'ui_right'")

    # You can continue testing other aspects of the movement logic in a similar manner.

    # Clean up
    character.queue_free()