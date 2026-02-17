from manim import *

class GeometricTransformations(Scene):
    def construct(self):
        # ----------- Scene Setup -----------
        plane = NumberPlane(
            x_range=[-6, 6, 1],
            y_range=[-4, 4, 1],
            background_line_style={"stroke_opacity": 0.4}
        )
        self.play(Create(plane))
        
        title = Text("Geometric Transformations", font_size=42)
        subtitle = Text("Translation - Reflection - Rotation - Central Symmetry", font_size=26).next_to(title, DOWN)
        self.play(Write(title), Write(subtitle))
        self.wait(2)
        self.play(FadeOut(title), FadeOut(subtitle))

        # ----------- Triangle -----------
        triangle = Polygon(
            [-2, -1, 0],
            [-1, 1, 0],
            [0, -1, 0],
            color=YELLOW
        )
        triangle_label = Text("Triangle", font_size=26).next_to(triangle, DOWN)
        self.play(Create(triangle), Write(triangle_label))
        self.wait(1)

        # ----------- Translation -----------
        trans_title = Text("1) Translation", font_size=34).to_edge(UP)
        trans_formula = MathTex(r"(x,y) \rightarrow (x+3,\ y+2)").next_to(trans_title, DOWN)
        self.play(Write(trans_title), Write(trans_formula))
        self.wait(1)

        self.play(triangle.animate.shift(RIGHT*3 + UP*2), run_time=2)
        self.play(triangle_label.animate.shift(RIGHT*3 + UP*2), run_time=2)
        self.wait(1)

        self.play(FadeOut(trans_title), FadeOut(trans_formula))

        # ----------- Reflection about y-axis -----------
        refl_title = Text("2) Reflection about y-axis", font_size=34).to_edge(UP)
        refl_formula = MathTex(r"(x,y) \rightarrow (-x,\ y)").next_to(refl_title, DOWN)
        y_axis = Line(plane.c2p(0, -4), plane.c2p(0, 4), color=BLUE)

        self.play(Write(refl_title), Write(refl_formula), Create(y_axis))
        self.wait(1)

        self.play(triangle.animate.flip(axis=UP).shift(LEFT*6), run_time=2)
        self.play(triangle_label.animate.shift(LEFT*6), run_time=2)
        self.wait(1)

        self.play(FadeOut(refl_title), FadeOut(refl_formula), FadeOut(y_axis))

        # ----------- Rotation 90 degrees -----------
        rot_title = Text("3) Rotation 90° about origin", font_size=34).to_edge(UP)
        rot_formula = MathTex(r"(x,y) \rightarrow (-y,\ x)").next_to(rot_title, DOWN)
        origin_dot = Dot(plane.c2p(0, 0), color=RED)
        origin_label = Text("O", font_size=26).next_to(origin_dot, DOWN)

        self.play(Write(rot_title), Write(rot_formula), FadeIn(origin_dot), Write(origin_label))
        self.wait(1)

        self.play(Rotate(triangle, angle=PI/2, about_point=plane.c2p(0,0)), run_time=2)
        self.play(Rotate(triangle_label, angle=PI/2, about_point=plane.c2p(0,0)), run_time=2)
        self.wait(1)

        self.play(FadeOut(rot_title), FadeOut(rot_formula))

        # ----------- Central Symmetry (180 rotation) -----------
        cs_title = Text("4) Central Symmetry (180°)", font_size=34).to_edge(UP)
        cs_formula = MathTex(r"(x,y) \rightarrow (-x,\ -y)").next_to(cs_title, DOWN)

        self.play(Write(cs_title), Write(cs_formula))
        self.wait(1)

        self.play(Rotate(triangle, angle=PI, about_point=plane.c2p(0,0)), run_time=2)
        self.play(Rotate(triangle_label, angle=PI, about_point=plane.c2p(0,0)), run_time=2)
        self.wait(1)

        self.play(FadeOut(cs_title), FadeOut(cs_formula), FadeOut(origin_dot), FadeOut(origin_label))

        # ----------- Congruence / Isometry -----------
        iso_title = Text("5) Isometry / Congruence", font_size=34).to_edge(UP)
        iso_text = Text("Translation, Reflection, Rotation keep lengths and angles.", font_size=24).next_to(iso_title, DOWN)

        self.play(Write(iso_title), Write(iso_text))
        self.wait(2)
        self.play(FadeOut(iso_title), FadeOut(iso_text))

        # ----------- Linear Transformation -----------
        lin_title = Text("6) Linear Transformation", font_size=34).to_edge(UP)
        lin_formula = MathTex(r"(x,y) \rightarrow (2x,\ y)").next_to(lin_title, DOWN)

        self.play(Write(lin_title), Write(lin_formula))
        self.wait(1)

        # Stretch effect
        self.play(triangle.animate.stretch(2, 0), run_time=2)
        self.wait(1)

        warning = Text("⚠ Lengths change → Not always congruent!", font_size=26, color=RED).to_edge(DOWN)
        self.play(Write(warning))
        self.wait(2)

        self.play(FadeOut(lin_title), FadeOut(lin_formula), FadeOut(warning))

        # ----------- Summary -----------
        summary = Text("Summary", font_size=40).to_edge(UP)
        s1 = Text("✓ Translation, Reflection, Rotation, Central Symmetry = Isometry", font_size=26).next_to(summary, DOWN)
        s2 = Text("⚠ Linear Transformation may change lengths.", font_size=26).next_to(s1, DOWN)

        self.play(Write(summary), Write(s1), Write(s2))
        self.wait(3)

        self.play(FadeOut(summary), FadeOut(s1), FadeOut(s2), FadeOut(triangle), FadeOut(triangle_label), FadeOut(plane))
