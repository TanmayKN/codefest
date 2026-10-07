# TrashSort

Built for CodeFest, February 2026.

A trash sorting system: a camera classifies waste as wet or dry, an Arduino sends it to the right bin, and a web dashboard shows how full each bin is.

## How it works

- `sort/` - Python script that reads the webcam with OpenCV, runs a Keras image model (wet waste / dry waste / nothing), and sends `w` or `d` to the Arduino over serial when it is more than 80% confident.
- `arduino/` - Arduino sketches. One servo swings a diverter toward the wet or dry side, two more servos open the bin flaps, and ultrasonic sensors report distance readings for each bin.
- `webpage/` - "Trash Monitor" dashboard (React + Vite) with a small Flask server that reads the sensor readings from the Arduino and serves them at `/api/data`. The page turns them into fill levels and refreshes every 5 seconds.

## Running it

Sorter (Python 3.10):

```
cd sort
pip install tensorflow opencv-python numpy pyserial
python main.py
```

Press Esc to quit.

Dashboard:

```
cd webpage
npm install
npm run dev
```

Dashboard backend:

```
cd webpage/src
pip install -r requirements.txt pyserial
python main.py
```

Flash the sketches in `arduino/` with the Arduino IDE (they use the Servo library).

Note: the serial port is hard-coded as `/dev/cu.usbmodem11101` in both Python files. Change it to your Arduino's port.

## Team

- TanmayKN
- ControlAlternateDel
- Cringenerd56
- GOLDphantomVex495

Parts of the project were written on shared laptops during the event, so the commit history does not map exactly to who wrote what.

Original repository: https://github.com/ControlAlternateDel/trashsort
