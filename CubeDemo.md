# Introduction #

Companion cube.c demo.


---


<table width='100%'>
<blockquote><tr>
<blockquote><td align='center'>
<blockquote><wiki:gadget url="http://goo.gl/Uql18" width="728" height="90" border="1" up_ad_client="1499394790009918" up_ad_slot="0061131168" up_ad_width="728" up_ad_height="90" /><br>
</blockquote></td>
</blockquote></tr>
</table></blockquote>


---


# Details #

```
// ml: cube test
// Copyright (C) 2012 Juan Manuel Borges Caño

// This program is free software: you can redistribute it and/or modify
// it under the terms of the GNU General Public License as published by
// the Free Software Foundation, either version 3 of the License, or
// (at your option) any later version.

// This program is distributed in the hope that it will be useful,
// but WITHOUT ANY WARRANTY; without even the implied warranty of
// MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
// GNU General Public License for more details.

// You should have received a copy of the GNU General Public License
// along with this program.  If not, see <http://www.gnu.org/licenses/>.

#include <stdlib.h>
#include <ML/ml.h>
#include <GL/freeglut.h>
#include <AL/alut.h>

#define TICKS 1 // (1.0f / mlStreamVideoFrequency())

unsigned int str, rot = 0;
ALuint src, bfrs[3];
GLuint tex;

void
Reshape(int width, int height)
{
	glViewport(0, 0, width, height); 
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	gluPerspective(45.0f, (float) width / (float) height, 0.1f, 10.0f);
	glMatrixMode(GL_MODELVIEW);
}

void
Keyboard(unsigned char key, int x, int y)
{
	switch(key)
	{
		case 27: glutLeaveMainLoop(); break;
		case 'p': alSourcePause(src); break;
		case ' ': mlStreamSync(); alSourcePlay(src); break;
	}
}

void
Special(int key, int x, int y)
{
	switch(key)
	{
		case GLUT_KEY_UP:
			if(mlStreamSeek(mlStreamDuration() - 5000))
			{
				ALint prc;
				ALuint prcs[3];
				unsigned int i;

				alSourceStop(src);
				alGetSourcei(src, AL_BUFFERS_PROCESSED, &prc);
				alSourceUnqueueBuffers(src, prc, prcs);
				for(i = 0; i < 3 && !mlStreamAudioEnd(); i++)
					mlStreamConvertBufferChunk(65536, bfrs[i]);
				alSourceQueueBuffers(src, i, bfrs);
				mlStreamReadFrame();
				mlStreamSync();
				if(mlStreamFrameCheck())
					mlStreamConvertTexSubImage2D(GL_TEXTURE_2D, 0, 0, 0);
				alSourcePlay(src);
			}
			break;
		case GLUT_KEY_RIGHT:
			if(mlStreamSeek(mlStreamTime() + mlStreamDuration() / 5))
			{
				ALint prc;
				ALuint prcs[3];
				unsigned int i;

				alSourceStop(src);
				alGetSourcei(src, AL_BUFFERS_PROCESSED, &prc);
				alSourceUnqueueBuffers(src, prc, prcs);
				for(i = 0; i < 3 && !mlStreamAudioEnd(); i++)
					mlStreamConvertBufferChunk(65536, bfrs[i]);
				alSourceQueueBuffers(src, i, bfrs);
				mlStreamReadFrame();
				mlStreamSync();
				if(mlStreamFrameCheck())
					mlStreamConvertTexSubImage2D(GL_TEXTURE_2D, 0, 0, 0);
				alSourcePlay(src);
			}
			break;
		case GLUT_KEY_LEFT:
			if(mlStreamSeek(mlStreamTime() - mlStreamDuration() / 20))
			{
				ALint prc;
				ALuint prcs[3];
				unsigned int i;

				alSourceStop(src);
				alGetSourcei(src, AL_BUFFERS_PROCESSED, &prc);
				alSourceUnqueueBuffers(src, prc, prcs);
				for(i = 0; i < 3 && !mlStreamAudioEnd(); i++)
					mlStreamConvertBufferChunk(65536, bfrs[i]);
				alSourceQueueBuffers(src, i, bfrs);
				mlStreamReadFrame();
				mlStreamSync();
				if(mlStreamFrameCheck())
					mlStreamConvertTexSubImage2D(GL_TEXTURE_2D, 0, 0, 0);
				alSourcePlay(src);
			}
			break;
	}
}

void
Display(void)
{
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	glLoadIdentity();
	gluLookAt(0.0f, 0.0f, 2.0f, 0.0f, 0.0f, 0.0f, 0.0f, 1.0f, 0.0f);
	glRotatef((float) rot, 0.0f, 1.0f, 0.0f);
	glBegin(GL_QUADS);
	glTexCoord2f(0.0f, 0.0f); glVertex3f(-0.5f, 0.5f, 0.5);
	glTexCoord2f(0.0f, 1.0f); glVertex3f(-0.5f, -0.5f, 0.5);
	glTexCoord2f(1.0f, 1.0f); glVertex3f(0.5f, -0.5f, 0.5);
	glTexCoord2f(1.0f, 0.0f); glVertex3f(0.5f, 0.5f, 0.5);
	glTexCoord2f(0.0f, 0.0f); glVertex3f(0.5f, 0.5f, 0.5);
	glTexCoord2f(0.0f, 1.0f); glVertex3f(0.5f, -0.5f, 0.5);
	glTexCoord2f(1.0f, 1.0f); glVertex3f(0.5f, -0.5f, -0.5);
	glTexCoord2f(1.0f, 0.0f); glVertex3f(0.5f, 0.5f, -0.5);
	glTexCoord2f(0.0f, 0.0f); glVertex3f(0.5f, 0.5f, -0.5);
	glTexCoord2f(0.0f, 1.0f); glVertex3f(0.5f, -0.5f, -0.5);
	glTexCoord2f(1.0f, 1.0f); glVertex3f(-0.5f, -0.5f, -0.5);
	glTexCoord2f(1.0f, 0.0f); glVertex3f(-0.5f, 0.5f, -0.5);
	glTexCoord2f(0.0f, 0.0f); glVertex3f(-0.5f, 0.5f, -0.5);
	glTexCoord2f(0.0f, 1.0f); glVertex3f(-0.5f, -0.5f, -0.5);
	glTexCoord2f(1.0f, 1.0f); glVertex3f(-0.5f, -0.5f, 0.5);
	glTexCoord2f(1.0f, 0.0f); glVertex3f(-0.5f, 0.5f, 0.5);
	glEnd();
	glutSwapBuffers();
}

void
Timer(int value)
{
	ALint state, prc;
	ALuint prcs[3];
	unsigned int i;

	alGetSourcei(src, AL_SOURCE_STATE, &state);
	if(state == AL_PLAYING || state == AL_PAUSED)
	{
		if(state == AL_PLAYING)
		{
			alGetSourcei(src, AL_BUFFERS_PROCESSED, &prc);
			alSourceUnqueueBuffers(src, prc, prcs);
			for(i = 0; i < prc && !mlStreamAudioEnd(); i++)
				mlStreamConvertBufferChunk(65536, prcs[i]);
			alSourceQueueBuffers(src, i, prcs);
			if(!mlStreamVideoEnd())
			{
				mlStreamReadFrame();
				if(mlStreamFrameCheck())
					mlStreamConvertTexSubImage2D(GL_TEXTURE_2D, 0, 0, 0);
			}
		}

		rot = (rot + 1) % 360;

		glutPostRedisplay();
		glutTimerFunc(TICKS, Timer, 0);
	}
	else glutLeaveMainLoop();
}

void
Load(int *argc, char **argv, const char *filepath)
{
	int x, y, width, height;
	unsigned int i;

	alutInit(argc, argv);
	glutInit(argc, argv);
	width = glutGet(GLUT_SCREEN_WIDTH) * 3 / 4;
	height = glutGet(GLUT_SCREEN_HEIGHT) * 3 / 4;
	x = (glutGet(GLUT_SCREEN_WIDTH) - width) / 2;
	y = (glutGet(GLUT_SCREEN_HEIGHT) - height) / 2;
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGBA | GLUT_DEPTH);
	glutInitWindowPosition(x, y);
	glutInitWindowSize(width, height);
	glutCreateWindow("ML Cube Demo");
	mlStreamCreate();

	glEnable(GL_CULL_FACE);
	glCullFace(GL_BACK);
	glEnable(GL_DEPTH_TEST);
	glEnable(GL_TEXTURE_2D);

	mlGenStreams(1, &str);
	mlBindStream(str);
	mlStreamLoadDefault(filepath);
	mlStreamConvert(AL_FORMAT_STEREO16, 44100, 128, 128, GL_RGB, GL_UNSIGNED_BYTE);

	alGenSources(1, &src);
	alGenBuffers(3, bfrs);

	glGenTextures(1, &tex);
	glBindTexture(GL_TEXTURE_2D, tex);
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
	glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
	glTexGeni(GL_S, GL_TEXTURE_GEN_MODE, GL_OBJECT_LINEAR);
	glTexGeni(GL_T, GL_TEXTURE_GEN_MODE, GL_OBJECT_LINEAR);
	glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, 128, 128, 0, GL_RGBA, GL_UNSIGNED_BYTE, NULL);

	for(i = 0; i < 3 && !mlStreamAudioEnd(); i++)
		mlStreamConvertBufferChunk(65536, bfrs[i]);
	alSourceQueueBuffers(src, i, bfrs);
	mlStreamReadFrame();
	mlStreamSync();
	if(mlStreamFrameCheck())
		mlStreamConvertTexSubImage2D(GL_TEXTURE_2D, 0, 0, 0);
	alSourcePlay(src);

	glutDisplayFunc(Display);
	glutReshapeFunc(Reshape);
	glutKeyboardFunc(Keyboard);
	glutSpecialFunc(Special);

	glutTimerFunc(TICKS, Timer, 0);
}

void
Unload(void)
{
	ALint prc;
	ALuint prcs[3];

	glDeleteTextures(1, &tex);

	alSourceStop(src);
	alGetSourcei(src, AL_BUFFERS_PROCESSED, &prc);
	alSourceUnqueueBuffers(src, prc, prcs);
	alDeleteBuffers(3, bfrs);
	alDeleteSources(1, &src);

	mlStreamUnload();
	mlDeleteStreams(1, &str);

	mlStreamDestroy();
	alutExit();
}

int
main(int argc, char **argv)
{
	if(argc == 2)
	{
		Load(&argc, argv, argv[1]);
		atexit(Unload);
		glutMainLoop();
	}

	return EXIT_SUCCESS;
}
```


---


<table width='100%'>
<blockquote><tr>
<blockquote><td align='center'>
<blockquote><wiki:gadget url="http://goo.gl/Uql18" width="728" height="90" border="1" up_ad_client="1499394790009918" up_ad_slot="0061131168" up_ad_width="728" up_ad_height="90" /><br>
</blockquote></td>
</blockquote></tr>
</table>