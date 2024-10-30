from ursina import *
from ursina.prefabs.first_person_controller import FirstPersonController

# Initialiser le jeu
app = Ursina()

# Fonction pour créer un bloc
class Voxel(Button):
    def __init__(self, position=(0,0,0)):
        super().__init__(
            parent=scene,
            position=position,
            model='cube',
            origin_y=0.5,
            texture='grass_block',
            color=color.color(0, 0, random.uniform(0.9, 1)),
            scale=0.5
        )

    def input(self, key):
        if self.hovered:
            # Clic gauche pour supprimer un bloc
            if key == 'left mouse down':
                destroy(self)
            # Clic droit pour ajouter un bloc
            if key == 'right mouse down':
                voxel = Voxel(position=self.position + mouse.normal)

# Générer un terrain de blocs
for x in range(8):
    for z in range(8):
        voxel = Voxel(position=(x,0,z))

# Ajouter un joueur avec contrôle à la première personne
player = FirstPersonController()

# Lancer l'application
app.run()

